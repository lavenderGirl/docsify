## 移动上拉加载
```javascript
var goLoadData = true; //控制页面 滚动的时候 一次请求一遍  无数据时 goLoadData = false;
$(document).ready(function(){
    $('body').scroll(function(e) {  
        if ((this.scrollHeight - (this.scrollTop + this.clientHeight)  < 200 )){
            if(goLoadData){
                //加载下一页数据
                //reqjson.pageNumber++;
                //packageMarketItem();
                goLoadData = false;
            }   
        }else{
            // 没有滚动到底端TODO 其他处理
        }
    }); 
});
```
## axios全局设置 
```js
//授权过期后axios操作跳转到登录页的一种全局处理方式 
axios.interceptors.request.use(
    config => {
        //如果 requestedWith 为 null，则为同步请求。
        //设置 requestedWith 为 XMLHttpRequest 则为 Ajax 请求。
        config.headers['X-Requested-With'] = 'XMLHttpRequest';
        return config
    },function(error){
        return Promise.reject(error)
    }
)
axios.interceptors.response.use(function (response) {
    return response
}, function (error) {
    if (error.response.status == 401){
        window.location.href="/admin/login";
    }
    if (error.response.status == 403){
        alert("对不起，您的权限不足");
    }
    if (error.response.status == 600){
        commonJs.alert({text:'网络异常'});
    }
    if (error.response.status == 601){
        commonJs.alert({text:'网络异常'});
    }
    //return Promise.reject(error)
})
```
## ajaxSetup()为ajax请求瘦身
```javascript
/*  当页面有很多ajax请求，且这些请求的参数比如url、type、dataType都一样，
    你会在每个请求里把这些参数都写一遍还是另辟蹊径？其实ajax有一个ajaxSetup方法，
    它就是用来设置全局ajax默认选项的。有了它，再也不用在每个ajax请求中把相同的参数都写一遍了。
*/
$.ajaxSetup({
    url: '/api/',
    type: 'post',
    dataType: 'json',
    error: function() {
        alert('调用接口失败');
        return false;
    }
});
/*  此外，还有一个经常遇到的场景——在每次请求开始的时候，
    需要显示一个loading动画，当请求结束时动画隐藏。
    对于这个，jQuery也是有封装好了的方法供我们去使用哒。
*/
$('#loading').ajaxStart(function(){
    $(this).show();
}).ajaxStop(function(){
    $(this).hide();
});

//例如：
$.ajaxSetup({
    dataType:"json",
    timeout:10000,
    statusCode:{
        401:function(data){
            location.href="/admin/login";
        },
        403:function(data){
            alert("对不起，您的权限不足");
        },
        600:function(){
            commonJs.alert({text:'网络异常'});
        },
        601:function(){
            commonJs.alert({text:'网络异常'});
        },
    }
});

var commonJs = {
    post:function(url,data,success,error,timeout,before,compelete){
        commonJs.ajax('POST',url,data,success,error,timeout,before,compelete);
    },
    get:function(url,data,success,error,timeout,before,compelete){
        commonJs.ajax('GET',url,data,success,error,timeout,before,compelete);
    },
    ajax:function(type,url,data,success,error,timeout,before,compelete){
        if(!timeout){
            timeout=10000;
        }
        $.ajax({
            timeout:timeout,
            url:url,
            type:type,
            data:data,
            dataType:'json',
            success:function(data){
                if(data){
                    switch(data.code){
                        case 200:
                            if($.isFunction(success)){
                                success(data);
                            }
                            break;
                        case 400:
                            if($.isFunction(error)){
                                error(data);
                            }else{
                                if(data.msg){
                                    alert(data.msg);
                                }
                            }
                            break;
                        default:
                            if($.isFunction(error)){
                                error(data);
                            }else{
                                if(data.msg){
                                    alert(data.msg);
                                }
                            }
                            break;
                    }
                }
            },
            error:function(){
            	  if($.isFunction(error)){
                      try{error()}catch(error){};
                      return;
                  }
            }
        });
    }
}
```
## 判断是否为Iphone X
```
// 如何判断是不是Iphone X
function(){
    return /iphone/gi.test(navigator.userAgent) && (screen.height == 812 && screen.width == 375)
}
```
## 判断是PC还是Mobile

```
function(){
    var userAgentInfo = navigator.userAgent;
    var Agents = ["Android", "iPhone","SymbianOS", "Windows Phone","iPad", "iPod"];
    var flag = true;
    for (var v = 0; v < Agents.length; v++) {
    	if (userAgentInfo.indexOf(Agents[v]) > 0) {
        	flag = false;
        	break;
    	}
    }
    return flag;
}
```
## js动态生成二维码
```
<!-- html -->
<div id="qrcode" style="width:200px; height:200px;position: fixed;bottom: 40%; right: 20%;"></div>

<!--引入外部js文件 -->
<script src="QRCode.js"></script>

<!-- 方法调用 -->
var qrcode = new QRCode(document.getElementById("qrcode"), { width : 200,height : 200 }); 
var token='params';
var QRCodeUrl='http:\\www.baidu.com'+'/Share/ScanQRCode?token='+token;
qrcode.makeCode(QRCodeUrl); 

<!--QRCode.js文件-->
下载地址：http://files.cnblogs.com/files/weishuanbao/QRCode.js
```
## 添加水印背景
````
<!-- html -->
<canvas id="myCanvas"></canvas>

<!--css -->
#myCanvas {
       position: absolute;
       z-index: 1000;
       pointer-events: none; 
 }

<!-- js -->
    $(window).resize(resizeCanvas);
    function resizeCanvas() {
        var canvas = document.getElementById("myCanvas");
        canvas.width = $(document).width();
        canvas.height = $(document).height();
        init();
    };
    resizeCanvas();
    function init() {
        var doWidth = $(document).width();
        var doHeight = $(document).height();
        //获取Canvas对象(画布)
        var canvas = document.getElementById("myCanvas");
        //简单地检测当前浏览器是否支持Canvas对象，以免在一些不支持html5的浏览器中提示语法错误
        if (canvas.getContext) {
            //获取对应的CanvasRenderingContext2D对象(画笔)
            var ctx = canvas.getContext("2d");
            //设置字体样式
            ctx.font = "italic small-caps 32px arial";
            //设置字体填充颜色
            ctx.fillStyle = "rgba(220,220,220, .36)";
            //向上旋转5度
            ctx.rotate(-5 * Math.PI / 180);
            //从坐标点(50,50)开始绘制文字
            var name = '[保密].'+$("#username").val()+$("#txtJobnumber").val();
            //var heightcount = Math.floor(doHeight / 10);
            //var widthcount = Math.floor(doWidth / 8);
            for (var j = -400; j < doHeight; j = j + 200) {
                for (var i = -400; i < doWidth ; i = i + 420) {
                    ctx.fillText(name, i, j);
                }
            }
        }
    }
````
## 数字转换成中文
[网上地址](http://www.cnblogs.com/breakdown/archive/2012/09/20/2689306.html1111#)
```javascript
   var digitaCconversion = {
        ary0: ["零", "一", "二", "三", "四", "五", "六", "七", "八", "九"],
        ary1: ["", "十", "百", "千"],
        ary2: ["", "万", "亿", "兆"],
        init: function (name) {
            this.name = name;
            return this.pri_ary();
        },
        strrev: function () {
            var ary = []
            for (var i = this.name.length; i >= 0; i--) {
                ary.push(this.name[i])
            }
            return ary.join("");
        }, //倒转字符串。
        pri_ary: function () {
            var $this = this
            var ary = this.strrev();
            var zero = ""
            var newary = ""
            var i4 = -1
            for (var i = 0; i < ary.length; i++) {
                if (i % 4 == 0) { //首先判断万级单位，每隔四个字符就让万级单位数组索引号递增
                    i4++;
                    newary = this.ary2[i4] + newary; //将万级单位存入该字符的读法中去，它肯定是放在当前字符读法的末尾，所以首先将它叠加入$r中，
                    zero = ""; //在万级单位位置的“0”肯定是不用的读的，所以设置零的读法为空

                }
                //关于0的处理与判断。
                if (ary[i] == '0') { //如果读出的字符是“0”，执行如下判断这个“0”是否读作“零”
                    switch (i % 4) {
                        case 0:
                            break;
                            //如果位置索引能被4整除，表示它所处位置是万级单位位置，这个位置的0的读法在前面就已经设置好了，所以这里直接跳过
                        case 1:
                        case 2:
                        case 3:
                            if (ary[i - 1] != '0') {
                                zero = "零"
                            }; //如果不被4整除，那么都执行这段判断代码：如果它的下一位数字（针对当前字符串来说是上一个字符，因为之前执行了反转）也是0，那么跳过，否则读作“零”
                            break;
                    }
                    newary = zero + newary;
                    zero = '';
                }
                else { //如果不是“0”
                    if (ary.length == 2 && i == 1 && ary[1] == '1') { this.ary0[parseInt(ary[i])] = ''; }; //去掉10到19前面的‘一’
                    newary = this.ary0[parseInt(ary[i])] + this.ary1[i % 4] + newary; //就将该当字符转换成数值型,并作为数组ary0的索引号,以得到与之对应的中文读法，其后再跟上它的的一级单位（空、十、百还是千）最后再加上前面已存入的读法内容。
                }
            }
            if (newary.indexOf("零") == 0) {
                newary = newary.substr(1)
            }//处理前面的0
            return newary;
        }
    };
    
    //用法：digitaCconversion.init('12');  输出为 ‘十二’
```
## JS获取浏览器名字及版本号

工作中需要通过JS去获取当前使用的浏览器的名字以及版本号，网上大堆资料都有一个关键词是 navigator.appName，但是这个方法获取的浏览器的名字只有两种要么是IE要么就是Netscap，倒是可以用来判断是否使用了IE，但是我想获取具体的浏览器产品名字比如  Firefox，Chrome等。所以只好通过navigator.userAgent，但是这个字符串是非常长的，分析他的特征，通过正则表达式来解决这个问题是不错的方法。

* 获取浏览器名字+版本字符串

```
function getBrowserInfo() {
    var agent = navigator.userAgent.toLowerCase();
    var regStr_ie = /msie [\d.]+;/gi;
    var regStr_ff = /firefox\/[\d.]+/gi
    var regStr_chrome = /chrome\/[\d.]+/gi;
    var regStr_saf = /safari\/[\d.]+/gi;
    //IE
    if (agent.indexOf("msie") > 0) {
        return agent.match(regStr_ie);
    }
    //firefox
    if (agent.indexOf("firefox") > 0) {
        return agent.match(regStr_ff);
    }
    //Chrome
    if (agent.indexOf("chrome") > 0) {
        return agent.match(regStr_chrome);
    }
    //Safari
    if (agent.indexOf("safari") > 0 && agent.indexOf("chrome") < 0) {
        return agent.match(regStr_saf);
    }
}
```

* 然后获取版本号

```
var browser = getBrowserInfo() ;
alert(browser);  //browser 为当前浏览器名称以及版本号
var verinfo = (browser+"").replace(/[^0-9.]/ig,""); //verinfo 为当前浏览器版本号
```
## 数组去重
[更多方法](https://segmentfault.com/a/1190000005116655)
```
//1.  最简单的方法就是利用 ES6 的 Set 
var s = new Set([1, 2, 3, 3, '3']);  // Set {1, 2, 3, "3"}
Array.from(s);  // 输出为：[1, 2, 3, "3"]

//2. 利用 filter 可以巧妙地去除 Array 的重复元素
var r,arr = ['apple', 'strawberry','awgpearkhl', 'banana', 'pear', 'apple', 'orange', 'orange', 'strawberry'];
r = arr.filter(function (element, index, self){
    return self.indexOf(element) === index;
});
r;
```
## 千位分隔符
```
<!-- 1. 使用正则表达式  下面语句都输出为： "123,456,789" -->
String(123456789).replace(/(\d)(?=(\d{3})+$)/g, "$1,");   
    
<!-- 2.使用toLocaleString()方法 -->
(123456789).toLocaleString('en-US');
```

## 文字列表循环向上滚动
```js
(function($){
    $.fn.myScroll = function(options){
        var defaults = {
            speed:40,  
            rowHeight:24 
        };
        var opts = $.extend({}, defaults, options), intId = [];
        function marquee(obj, step){
            obj.find("ul").animate({ marginTop: '-=1'},0,function(){
                var s = Math.abs(parseInt($(this).css("margin-top")));
                if(s >= step){
                    $(this).find("li").slice(0, 1).appendTo($(this));
                    $(this).css("margin-top", 0);
                }
            });
        }
        this.each(function(i){
            var sh = opts["rowHeight"], speed = opts["speed"], _this = $(this);
            intId[i] = setInterval(function(){
                if(_this.find("ul").height()<=_this.height()){
                    clearInterval(intId[i]);
                }else{
                    marquee(_this, sh);
                }
            }, speed);

            _this.hover(function(){
                clearInterval(intId[i]);
            },function(){
                intId[i] = setInterval(function(){
                    if(_this.find("ul").height()<=_this.height()){
                        clearInterval(intId[i]);
                    }else{
                        marquee(_this, sh);
                    }
                }, speed);
            });
        });
    }
})(jQuery);

$(function(){
    var _h  = $("div.list_lh li").height();
    _h = _h.toFixed(2);
    $("div.list_lh").myScroll({
        speed:20,   //数值越大，速度越慢
        rowHeight:_h  //li的高度
    });
});
```


## progress
```html
<div class="circleProgress_wrapper">
    <div class="wrapper right">
        <div class="circleProgress rightcircle"></div>
    </div>
    <div class="wrapper left">
        <div class="circleProgress leftcircle"></div>
    </div>
    <h2 class="number" id="number">10</h2>
</div>
```
```css
.circleProgress_wrapper{
    width: 182px;
    height: 182px;
    margin: 2.81rem auto;
    position: relative;
}
.wrapper{
    width: 91px;
    height: 182px;
    position: absolute;
    top:0;
    overflow: hidden;
}
.right{
    right:0;
}
.left{
    left:0;
}
.circleProgress{
    width: 166px;
    height: 166px;
    border:8px solid #6ce5cf;
    border-radius: 50%;
    position: absolute;
    top:0;
    -webkit-transform: rotate(-135deg);
}
.rightcircle{
    border-top:8px solid #fff;
    border-right:8px solid #fff;
    right:0;
    -webkit-animation: circleProgressLoad_right 5s linear infinite;
}
.leftcircle{
    border-bottom:8px solid #fff;
    border-left:8px solid #fff;
    left:0;
    -webkit-animation: circleProgressLoad_left 5s linear infinite;
}
@-webkit-keyframes circleProgressLoad_right{
    0%{
        -webkit-transform: rotate(-135deg);
    }
    50%,100%{
        -webkit-transform: rotate(45deg);
    }
}
@-webkit-keyframes circleProgressLoad_left{
    0%,50%{
        -webkit-transform: rotate(-135deg);
    }
    100%{
        -webkit-transform: rotate(45deg);
    }
}
```

## 三个小点动画：
```html
<div class="ball-pulse"><div></div><div></div><div></div></div>
```
```css
.ball-pulse {
    display: inline;
    margin-left: 7px;
}
.ball-pulse>div {
    background-color: #fff;
    border-radius: 100%;
    margin: 2px;
    display: inline-block
}
@-webkit-keyframes scale {
    0%,80% {
        -webkit-transform: scale(1);
        transform: scale(1);
        opacity: 1
    }
    45% {
        -webkit-transform: scale(.1);
        transform: scale(.1);
        opacity: .7
    }
}
@keyframes scale {
    0%,80% {
        -webkit-transform: scale(1);
        transform: scale(1);
        opacity: 1
    }
    45% {
        -webkit-transform: scale(.1);
        transform: scale(.1);
        opacity: .7
    }
}
.ball-pulse>div:nth-child(1) {
    -webkit-animation: scale .75s -.24s infinite cubic-bezier(.2,.68,.18,1.08);
    animation: scale .75s -.24s infinite cubic-bezier(.2,.68,.18,1.08)
}
.ball-pulse>div:nth-child(2) {
    -webkit-animation: scale .75s -.12s infinite cubic-bezier(.2,.68,.18,1.08);
    animation: scale .75s -.12s infinite cubic-bezier(.2,.68,.18,1.08)
}
.ball-pulse>div:nth-child(3) {
    -webkit-animation: scale .75s 0s infinite cubic-bezier(.2,.68,.18,1.08);
    animation: scale .75s 0s infinite cubic-bezier(.2,.68,.18,1.08)
}
.ball-pulse>div {
    width: 3px;
    height: 3px;
    -webkit-animation-fill-mode: both;
    animation-fill-mode: both
}
```

## 10秒倒计时：
```js
countDown(10,"number",function(){
    $('#number').html("9");           
});   
function  countDown(time, id, overFn){
    time = Number(time);
    var countTime = setInterval(function(){
        time--;
        $("#" + id).text(time);
        $("#" + id).attr("disabled",true);
        if(time == 0){
            $("#" + id).removeAttr("disabled");
            clearInterval(countTime);
            overFn();
        }
    },1000);
}
```

