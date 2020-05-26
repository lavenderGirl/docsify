
## h5 Video打开本地摄像头和离开页面关闭摄像头
```html
<video id="video" ref="video" width="640" height="480"></video>
<canvas id="canvas" ref="canvas" width="640" height="480"></canvas>
```
```js
methods:{
  clickToPhoto(){
      //点击把当前视频截图
      this.ctx.drawImage(this.video, 0, 0, this.video.clientWidth, this.video.clientHeight);
      this.photoUrl = this.canvas.toDataURL('image/png');
  },
  liveVideo(){
      this.video = this.$refs.video;
      this.canvas = this.$refs.canvas;
      this.ctx = this.canvas.getContext('2d');

      if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
          navigator.mediaDevices.getUserMedia({
              video: true,
          }).then((stream)=>{
              this.MediaStreamTrack=typeof stream.stop==='function'?stream:stream.getTracks()[0];
              this.video["srcObject"]=stream;
              this.video.play();
          }).catch((err)=>{
              console.log(err);
              //调用摄像头失败给的提示
          });
      }else{
          console.log('getUserMedia is not implemented in this browser');
      }
  },
  closeVideo(){ //关闭摄像头
      console.log(this.MediaStreamTrack);
      this.MediaStreamTrack && this.MediaStreamTrack.stop();
  }
}
```

##  pc和移动端获取滚动条的位置
```js
移动端获取滚动条:document.body.scrollTop
pc端获取滚动条:document.documentElement.scrollTop
```
## JS移动端判断上拉和下滑
``` js
    //滑动处理
var startX, startY;
document.addEventListener('touchstart',function (ev) {
    startX = ev.touches[0].pageX;
    startY = ev.touches[0].pageY;
}, false);

document.addEventListener('touchend',function (ev) {
    var endX, endY;
    endX = ev.changedTouches[0].pageX;
    endY = ev.changedTouches[0].pageY;
    var direction = GetSlideDirection(startX, startY, endX, endY);
    switch(direction) {
        case 0:
                alert("无操作");
            break;
        case 1:
            // 向上
            alert("up");
            break;
        case 2:
            // 向下
            alert("down");
            break;

        default:
    }
  }, false);

function GetSlideDirection(startX, startY, endX, endY) {
    var dy = startY - endY;
    //var dx = endX - startX;
    var result = 0;
    if(dy>0) {//向上滑动
        result=1;
    }else if(dy<0){//向下滑动
        result=2;
    }else{
        result=0;
    }
    return result;
  }
```

## 扫码枪读取条形码数据（vue）
扫码枪是模拟键盘输入的，所有事件为document.onkeypress = function(){}.
在vue项目中，是没有window.onload的，所以在created钩子函数中做：
```js
  var b = "";
  document.onkeydown = (event)=>{
    if (event.keyCode != 13) {
        var bizCode = String.fromCharCode(event.keyCode);
        // if (event.keyCode >= 48 && event.keyCode <= 122) {
            b = b + bizCode;
        // }
    } else {
        b = "";
    }
    this.barCode = b;
    // console.log('barcode:' + this.barCode);
    if(this.barCode.toString().length == 20){ //支付宝跟微信条形码都是18位
        //苹果电脑上测试时，条形码前面有两位未知码要去掉
        this.barCode = this.barCode.toString().slice(2);
        console.log('barCode应该输出18位：' + this.barCode)
        this.payFn();
    }else if(this.barCode.toString().length == 18){
        //在win电脑上条形码正常，不用做处理
        this.barCode = this.barCode.toString();
        console.log('barCode应该输出18位：' + this.barCode)
        this.payFn();
    }
  };
```
## js 验证手机号码和座机号码
```js
// checkTel('020-12345678') => true   checkTel('13590871234') => true 
function checkTel(tel) 
{
   var mobile = /^1[3|4|5|7|8][0-9]\d{8}$/ , phone = /^0\d{2,3}-?\d{7,8}$/;
   return mobile.test(tel) || phone.test(tel);
}
```
## 手机号中间四位显示星号
```js
function handelMobile(value){
  if(!value) return '';
  if(typeof value !== 'string') value = value.toString();
  return value.replace(/^(\d{3})\d*(\d{4})$/,'$1****$2');
}
// handelMobile(13923451241)  输出："139****1241"
```

## 日期格式化函数
```js
// 也可获取当前日期：formatTime(new Date())
function formatTime(d){ // 输出为 : 2019-10-08 17:50:44  星期二
    const year = d.getFullYear();
    const month = d.getMonth() + 1;
    const day = d.getDate();
    let days = d.getDay(); 
    const weeks = new Array("星期日", "星期一", "星期二", "星期三", "星期四", "星期五", "星期六");
    const week = weeks[days];
    const hour = d.getHours();
    const minute = d.getMinutes();
    const second = d.getSeconds();

    return [year, month, day].map(formatNumber).join('-') + ' ' + [hour, minute, second].map(formatNumber).join(':') + '  ' + week;
},
function formatNumber(n){
    n = n.toString()
    return n[1] ? n : '0' + n
}
```

## 清除空格
```js
// 清除所有空格
function removeAllSpace(str) {
    return str.replace(/\s+/g, "");
}

// 清除左空格/右空格
function ltrim(s){ return s.replace( /^(\s*|　*)/, ""); } 
function rtrim(s){ return s.replace( /(\s*|　*)$/, ""); }

```

## 复制文本内容到剪切板
```html
<div  id="copeText">12345678</div>
<input type="button" onClick="copyUrl()" value="点击复制代码" />
```
```js
function copeText(){
    var copeText=document.getElementById("copeText").innerText;
    var oInput = document.createElement('input');
        oInput.value = copeText;
        document.body.appendChild(oInput);
        oInput.select(); // 选择对象
        document.execCommand("Copy"); // 执行浏览器复制命令
        document.body.removeChild(oInput)
        // oInput.className = 'oInput';
        // oInput.style.display='none';
        // alert('复制成功');
}
```

## 前端生成文件并下载
```js
function createAndDownloadFile(fileName, content) {
    const aTag = document.createElement('a');
    const blob = new Blob([content]);
    aTag.download = `${fileName}.json`;
    aTag.href = URL.createObjectURL(blob);
    aTag.click();
    URL.revokeObjectURL(blob);
}

// 以下是一个例子，亲测有效
axios({ 
    method: 'post',
    url: url, 
    data: paramsObj, 
    responseType: 'blob' // 表明返回服务器返回的数据类型
}).then((res) => { // 处理返回的文件流
    let blob = new Blob([res.data], {type: "application/vnd.ms-excel"}); 
    const aLink = document.createElement('a');
    document.body.appendChild(aLink);
    aLink.style.display='none';
    const objectUrl = window.URL.createObjectURL(blob);
    aLink.href = objectUrl;
    aLink.download = '词云数据'; //下载后的文件名称
    aLink.click();
    document.body.removeChild(aLink);//这句是针对火狐的，没有这句话，火狐就根本导不出文件来，火狐对a.download似乎有点个人意见，但Chrome可以，折腾了好久。
})
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
        console.log("对不起，您的权限不足");
    }
    if (error.response.status == 600){
        console.log({text:'网络异常'});
    }
    if (error.response.status == 601){
        console.log({text:'网络异常'});
    }
    //return Promise.reject(error)
})
```

## 判断是否为Iphone X
```js
// 如何判断是不是Iphone X
function isIphoneX(){
    return /iphone/gi.test(navigator.userAgent) && (screen.height == 812 && screen.width == 375)
}
```

## 判断为IOS还是安卓
```js
// true：ios  false:android
function isIOSFn(){
    var isIOS = true;
    var u = navigator.userAgent, app = navigator.appVersion;
    var _isAndroid = u.indexOf('Android') > -1 || u.indexOf('Linux') > -1; //android终端或者uc浏览器
    var _isiOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端
    if(_isAndroid){
        isIOS = false;
    }
    if(_isiOS){
        isIOS = true;
    }
    return isIOS;
}
```


## 判断是PC还是Mobile

```js
function isPc(){
    //true:是PC端  false:是移动端
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
```html
<div id="qrcode"></div>
```
```css
#qrcode{
    width:200px; height:200px;position: fixed;bottom: 40%; right: 20%;
}
```
```js
// 引入外部js文件
// QRCode.js 是一个用于生成二维码的 JavaScript 库。主要是通过获取 DOM 的标签,再通过 HTML5 Canvas 绘制而成,不依赖任何库
<script src="QRCode.js"></script>

// 方法调用
var qrcode = new QRCode(document.getElementById("qrcode"), { width : 200,height : 200 }); 
var token='params';
var QRCodeUrl='http:\\www.baidu.com'+'/Share/ScanQRCode?token='+token;
qrcode.makeCode(QRCodeUrl); 

// QRCode.js文件
下载地址：http://files.cnblogs.com/files/weishuanbao/QRCode.js
```

## 数组去重
[更多方法](https://segmentfault.com/a/1190000005116655)
```js
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
```js
//1. 使用正则表达式  下面语句都输出为： "123,456,789"
String(123456789).replace(/(\d)(?=(\d{3})+$)/g, "$1,");   
    
//2.使用toLocaleString()方法
(123456789).toLocaleString('en-US');
```

## 如何判断一个变量是否为数组（isArray）

```js
// 1、instanceof
function isArray (obj) {
  return obj instanceof Array;
}

// 2、Array对象的 isArray方法
function isArray (obj) {
  return Array.isArray(obj);
}

// 3、Object.prototype.toString
function isArray (obj) {
  return Object.prototype.toString.call(obj) === '[object Array]';
}
```

## 将数字转换为大写金额

```js
   /**
 * 将数字转换为大写金额
 * @param Num 数值
 // 调用：changeToChinese(8998.2) 输出为："捌仟玖佰玖拾捌元贰角"
 * */
function changeToChinese(Num) {
  //判断如果传递进来的不是字符的话转换为字符
  if (typeof Num === "number")  Num = new String(Num);
  Num = Num.replace(/,/g, "") //替换tomoney()中的“,”
  Num = Num.replace(/ /g, "") //替换tomoney()中的空格
  Num = Num.replace(/￥/g, "") //替换掉可能出现的￥字符
  if (isNaN(Num)) return "";
  //字符处理完毕后开始转换，采用前后两部分分别转换
  var part = String(Num).split(".");
  var newchar = "";
  //小数点前进行转化
  for (var i = part[0].length - 1; i >= 0; i--) {
    if (part[0].length > 10) return "";
    var tmpnewchar = ""
    var perchar = part[0].charAt(i);
    switch (perchar) {
      case "0":
        tmpnewchar = "零" + tmpnewchar;
        break;
      case "1":
        tmpnewchar = "壹" + tmpnewchar;
        break;
      case "2":
        tmpnewchar = "贰" + tmpnewchar;
        break;
      case "3":
        tmpnewchar = "叁" + tmpnewchar;
        break;
      case "4":
        tmpnewchar = "肆" + tmpnewchar;
        break;
      case "5":
        tmpnewchar = "伍" + tmpnewchar;
        break;
      case "6":
        tmpnewchar = "陆" + tmpnewchar;
        break;
      case "7":
        tmpnewchar = "柒" + tmpnewchar;
        break;
      case "8":
        tmpnewchar = "捌" + tmpnewchar;
        break;
      case "9":
        tmpnewchar = "玖" + tmpnewchar;
        break;
    }
    switch (part[0].length - i - 1) {
      case 0:
        tmpnewchar = tmpnewchar + "元";
        break;
      case 1:
        if (perchar != 0) tmpnewchar = tmpnewchar + "拾";
        break;
      case 2:
        if (perchar != 0) tmpnewchar = tmpnewchar + "佰";
        break;
      case 3:
        if (perchar != 0) tmpnewchar = tmpnewchar + "仟";
        break;
      case 4:
        tmpnewchar = tmpnewchar + "万";
        break;
      case 5:
        if (perchar != 0) tmpnewchar = tmpnewchar + "拾";
        break;
      case 6:
        if (perchar != 0) tmpnewchar = tmpnewchar + "佰";
        break;
      case 7:
        if (perchar != 0) tmpnewchar = tmpnewchar + "仟";
        break;
      case 8:
        tmpnewchar = tmpnewchar + "亿";
        break;
      case 9:
        tmpnewchar = tmpnewchar + "拾";
        break;
    }
    var newchar = tmpnewchar + newchar;
  }
  //小数点之后进行转化
  if (Num.indexOf(".") != -1) {
    if (part[1].length > 2) {
      // alert("小数点之后只能保留两位,系统将自动截断");
      part[1] = part[1].substr(0, 2)
    }
    for (i = 0; i < part[1].length; i++) {
      tmpnewchar = ""
      perchar = part[1].charAt(i)
      switch (perchar) {
        case "0":
          tmpnewchar = "零" + tmpnewchar;
          break;
        case "1":
          tmpnewchar = "壹" + tmpnewchar;
          break;
        case "2":
          tmpnewchar = "贰" + tmpnewchar;
          break;
        case "3":
          tmpnewchar = "叁" + tmpnewchar;
          break;
        case "4":
          tmpnewchar = "肆" + tmpnewchar;
          break;
        case "5":
          tmpnewchar = "伍" + tmpnewchar;
          break;
        case "6":
          tmpnewchar = "陆" + tmpnewchar;
          break;
        case "7":
          tmpnewchar = "柒" + tmpnewchar;
          break;
        case "8":
          tmpnewchar = "捌" + tmpnewchar;
          break;
        case "9":
          tmpnewchar = "玖" + tmpnewchar;
          break;
      }
      if (i == 0) tmpnewchar = tmpnewchar + "角";
      if (i == 1) tmpnewchar = tmpnewchar + "分";
      newchar = newchar + tmpnewchar;
    }
  }
  //替换所有无用汉字
  while (newchar.search("零零") != -1)
    newchar = newchar.replace("零零", "零");
  newchar = newchar.replace("零亿", "亿");
  newchar = newchar.replace("亿万", "亿");
  newchar = newchar.replace("零万", "万");
  newchar = newchar.replace("零元", "元");
  newchar = newchar.replace("零角", "");
  newchar = newchar.replace("零分", "");
  if (newchar.charAt(newchar.length - 1) == "元") {
    newchar = newchar + "整"
  }
  return newchar;
}
```

## 将阿拉伯数字翻译成中文的大写数字
```js
/**
 * 将阿拉伯数字翻译成中文的大写数字
 * @param num 数字
 // numberToChinese(59999.12) 输出为："五萬九仟九百九十九点一二"
 * */

function numberToChinese(num) {
  var AA = new Array("零", "一", "二", "三", "四", "五", "六", "七", "八", "九", "十");
  var BB = new Array("", "十", "百", "仟", "萬", "億", "点", "");
  var a = ("" + num).replace(/(^0*)/g, "").split("."),
    k = 0,
    re = "";
  for (var i = a[0].length - 1; i >= 0; i--) {
    switch (k) {
      case 0:
        re = BB[7] + re;
        break;
      case 4:
        if (!new RegExp("0{4}//d{" + (a[0].length - i - 1) + "}$")
          .test(a[0]))
          re = BB[4] + re;
        break;
      case 8:
        re = BB[5] + re;
        BB[7] = BB[5];
        k = 0;
        break;
    }
    if (k % 4 == 2 && a[0].charAt(i + 2) != 0 && a[0].charAt(i + 1) == 0)
      re = AA[0] + re;
    if (a[0].charAt(i) != 0)
      re = AA[a[0].charAt(i)] + BB[k % 4] + re;
    k++;
  }

  if (a.length > 1) // 加上小数部分(如果有小数部分)
  {
    re += BB[6];
    for (var i = 0; i < a[1].length; i++)
      re += AA[a[1].charAt(i)];
  }
  if (re == '一十')
    re = "十";
  if (re.match(/^一/) && re.length == 3)
    re = re.replace("一", "");
  return re;
}
```

## JS获取浏览器名字及版本号

工作中需要通过JS去获取当前使用的浏览器的名字以及版本号，网上大堆资料都有一个关键词是 navigator.appName，但是这个方法获取的浏览器的名字只有两种要么是IE要么就是Netscap，倒是可以用来判断是否使用了IE，但是我想获取具体的浏览器产品名字比如  Firefox，Chrome等。所以只好通过navigator.userAgent，但是这个字符串是非常长的，分析他的特征，通过正则表达式来解决这个问题是不错的方法。

* 获取浏览器名字+版本字符串

```js
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

```js
var browser = getBrowserInfo() ;
alert(browser);  //browser 为当前浏览器名称以及版本号
var verinfo = (browser+"").replace(/[^0-9.]/ig,""); //verinfo 为当前浏览器版本号
```

## vue-cli 项目构建
在node.js 以及npm安装的前提下。用vue-cli脚手架简单构建一个项目。
- $ npm install -g vue-cli
- $ vue init webpack my-project
- $ cd my-project
- $ npm install
- $ npm run dev

## jq | 移动上拉加载
```js
//控制页面 滚动的时候 一次请求一遍  无数据时 goLoadData = false;
var goLoadData = true; 
$(document).ready(function(){
    $('body').scroll(function(e) {  
        if ((this.scrollHeight - (this.scrollTop + this.clientHeight)  < 200 )){
            if(goLoadData){
                //加载下一页数据
                goLoadData = false;
            }   
        }else{
            // 没有滚动到底端TODO 其他处理
        }
    }); 
});
```

## jq | ajaxSetup()为ajax请求瘦身
```js
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
            alert({text:'网络异常'});
        },
        601:function(){
            alert({text:'网络异常'});
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

## jq | 添加水印背景
```html
<canvas id="myCanvas"></canvas>
```
```css
#myCanvas {
    position: absolute;
    z-index: 1000;
    pointer-events: none; 
 }
```
```js
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
```

## jq | 文字列表循环向上滚动
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









