```js
(function(global, factory) {
    typeof define === 'function' && define.amd ?
        define(function() {
            return factory(global)
        }) :
        factory(global)
}(this, function(window) {
    'use strict';

    var undefined,
        win = window,
        doc = win.document,
        _DDC = {
            //初始化页面rem值
            init: (function() {
                var docEl = doc.documentElement,
                    clientWidth = doc.documentElement.clientWidth;
                if (!clientWidth) return
                docEl.style.fontSize = clientWidth >= 750 ?'100px':100 * (clientWidth / 750) + 'px'
            })(),

            //判断返回当前调试环境(当前为自动判断，特殊情况可在自己页面手动重置 _DDC.status 值)
            status: (function() {
                var _url = win.location.href;
                // 0开发环境  1测试环境  2stagng环境  3生产环境
                var _status = _url.indexOf('localhost') > -1 ? 0 : _url.indexOf('mobile-test') > -1 ? 1 : _url.indexOf('mobile-staging') > -1 ? 2 : 3;
                return _status
            })(),

            //获取URL参数
            getQueryString: function(name) {
                if (!name) return null
                var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
                var r = win.location.search == "" ? null : decodeURIComponent(win.location.search).substr(1).match(reg);
                if (r != null) return unescape(r[2]);
                return null
            },

            //判断客户端为安卓还是IOS
            client: function() {
                return /(iPhone|iPad|iPod|iOS)/i.test(navigator.userAgent) ? true : false
            },

            //判断手机号码是否合法
            isPhone: function(phone) {
                return (/^1\d{10}$/).test(phone) ? true : false
            },

            //判断邮箱是否合法
            isMail: function(mail) {
                var reg = /^[a-z0-9](\w|\.|-)*@([a-z0-9]+-?[a-z0-9]+\.){1,3}[a-z]{2,4}$/i;
                var email = mail.replace(/^\s+|\s+$/g, "").toLowerCase();
                return email.match(reg) ? true : false
            },

            //嵌入在app中关闭页面loading(防止兼容性问题，暂不使用promise)
            closeLoading: function() {
                if (!this.inApp()) return
                typeof ddcApp === 'object' && typeof ddcApp.closeLoading === 'function' ?
                    ddcApp.closeLoading() :
                    (function() {
                        var num = 0,
                            timer = setTimeout(function(){
                                if(typeof ddcApp == 'object'){
                                    typeof ddcApp.closeLoading == 'function' && ddcApp.closeLoading()
                                }else if(num < 30){
                                    num++
                                    timer()
                                }
                            },100)
                    })();
            },

            //是否IphoneX
            isIphoneX: function() {
                if (/(iPhone|iPad|iPod|iOS)/i.test(navigator.userAgent) && screen.width === 375 && screen.height === 812) {
                    //宽375，高812则为iPhoneX
                    return true
                } else {
                    return false
                }
            },

            //是否在微信中
            isWeiXin: function() {
                var ua = win.navigator.userAgent.toLowerCase();
                return ua.match(/MicroMessenger/i) == 'micromessenger' ? true : false
            },

            //是否在app中
            inApp: function() {
                var userAgent = navigator.userAgent;
                if (/daydaycook/.test(userAgent)) {
                    return true
                } else {
                    return false
                }
            },

            //弹窗样式
            dialog: function(text, type) {
                //type  1成功   2警告
                var box = doc.createElement('div');
                box.id = 'ddc-alert-box';
                box.className = 'ddc-alert-box';

                var _span = doc.createElement('span');
                _span.className = type == 1 ? 'ddc-success' : 'ddc-warning';
                var _p = doc.createElement('p');
                _p.className = 'ddc-icon';
                _p.appendChild(_span);

                var _p2 = doc.createElement('p');
                _p2.className = 'ddc-text';
                _p2.innerHTML = text;

                var _div = doc.createElement('div');
                _div.className = 'ddc-alert';

                _div.appendChild(_p);
                _div.appendChild(_p2);
                box.appendChild(_div);

                var _old = doc.querySelector('#ddc-alert-box');
                if (_old) _old.parentNode.removeChild(_old);
                doc.querySelector('body').appendChild(box);
            },

            //成功弹窗
            success: function(text, time) {
                this.dialog(text, 1);
                setTimeout(function() {
                    var _old = doc.querySelector('#ddc-alert-box');
                    if (_old) _old.parentNode.removeChild(_old);
                }, time || 2000)
            },

            //成功弹窗
            warning: function(text, time) {
                this.dialog(text, 2);
                setTimeout(function() {
                    var _old = doc.querySelector('#ddc-alert-box');
                    if (_old) _old.parentNode.removeChild(_old);
                }, time || 2000)
            },

            //加减乘除基础方法
            digitLength: function(num) {
                var eSplit = num.toString().split(/[eE]/);
                var len = (eSplit[0].split('.')[1] || '').length - (+(eSplit[1] || 0));
                return len > 0 ? len : 0;
            },

            //精确加法
            accAdd: function(num1, num2) {
                var baseNum = Math.pow(10, Math.max(this.digitLength(num1), this.digitLength(num2)));
                return (this.accMul(num1, baseNum) + this.accMul(num2, baseNum)) / baseNum;
            },

            //精确减法
            subtr: function(num1, num2) {
                var baseNum = Math.pow(10, Math.max(this.digitLength(num1), this.digitLength(num2)));
                return (this.accMul(num1, baseNum) - this.accMul(num2, baseNum)) / baseNum;
            },

            //精确乘法
            accMul: function(num1, num2) {
                var num1Changed = Number(num1.toString().replace('.', ''));
                var num2Changed = Number(num2.toString().replace('.', ''));
                var baseNum = this.digitLength(num1) + this.digitLength(num2);
                return num1Changed * num2Changed / Math.pow(10, baseNum);
            },

            //精确除法
            divide: function(num1, num2) {
                var num1Changed = Number(num1.toString().replace('.', ''));
                var num2Changed = Number(num2.toString().replace('.', ''));
                return this.accMul((num1Changed / num2Changed), Math.pow(10, this.digitLength(num2) - this.digitLength(num1)));
            },
            toFixedNo:function(num){
                var _num = num * 1000;
                var numStr = String(_num).split('.')[0];
                var lastBit = numStr.slice(numStr.length-1,numStr.length);
                if(lastBit == 5){
                    return  Math.ceil(num*100)/100;
                }else{
                    return  Math.round(num*100)/100;
                }
            },
            formatTime:function(d){ // 输出为 : 2019-10-08 17:50:44  星期二
                const year = d.getFullYear();
                const month = d.getMonth() + 1;
                const day = d.getDate();
                let days = d.getDay(); 
                const weeks = new Array("星期日", "星期一", "星期二", "星期三", "星期四", "星期五", "星期六");
                const week = weeks[days];
                const hour = d.getHours();
                const minute = d.getMinutes();
                const second = d.getSeconds();
            
                return [year, month, day].map(_DDC.formatNumber).join('-') + ' ' + [hour, minute, second].map(_DDC.formatNumber).join(':') + '  ' + week;
            },
            formatNumber:function(n){
                n = n.toString()
                return n[1] ? n : '0' + n
            }
        }

    win.addEventListener('orientationchange' in win ? 'orientationchange' : 'resize', _DDC.init, false);

    win._DDC = win.DDC || _DDC;
}));
```