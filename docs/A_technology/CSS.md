## 0.5px 
```css
.border-top,.border-bottom,.border-left,.border-right {
    position: relative;
}
.border-top:before,.border-bottom:before,.border-left:before,.border-right:before {
    content: '';
    position: absolute;
    left: 0;
    right: 0;
    width: 200%;
    height: 1px;
    -webkit-transform-origin: 0 0;
    -moz-transform-origin: 0 0;
    -ms-transform-origin: 0 0;
    -o-transform-origin: 0 0;
    transform-origin: 0 0;
    -webkit-transform: scale(0.5, 0.5);
    -ms-transform: scale(0.5, 0.5);
    -o-transform: scale(0.5, 0.5);
    transform: scale(0.5, 0.5);
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
}
.border-top:before{
    border-top: 1px solid #dedede;
    top: 0;
}
.border-bottom:before{
    border-bottom: 1px solid #dedede;
    bottom: 0;
}
.border-left:before{
    border-left: 1px solid #dedede;
    left: 0;
    top: 0;
    bottom: 0;
    height: 200%;
}
.border-right:before{
    border-right: 1px solid #dedede;
    right: 0;
    top: 0;
    bottom: 0;
    height: 200%;
}
``` 

## 淘宝选商品型号弹框 遮罩
```html
<section class="widgets-cover">
    <div class="cover-bg"></div>
    <div class="cover-content">
        <!-- content -->
    </div>
</section>
```
```css
.widgets-cover{
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 999;
    pointer-events: none;
    opacity: 0;
    transition: opacity .3s 80ms;
    will-change: opacity;
    bottom: var(--safe-area-inset-bottom);
    height: 100%;
}
.widgets-cover.show{
    pointer-events: auto;
    opacity: 1;
}
.cover-bg{
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    top: 0;
    background-color: rgba(0,0,0,.5);
}
.widgets-cover.show .cover-bg{
    background-color: rgba(0,0,0,.5);
}
.widgets-cover .cover-content {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    /* top: 20%; */
    background-color: #fff;
    -webkit-transition: -webkit-transform .3s cubic-bezier(0,0,.25,1) 80ms;
    transition: transform .3s cubic-bezier(0,0,.25,1) 80ms;
    -webkit-transform: translate3d(0,100%,0);
    transform: translate3d(0,100%,0);
    will-change: transform;
    box-shadow: 0 -1px 40px rgba(0,0,0,.3)
}
.widgets-cover.show .cover-content{
    -webkit-transform: translate3d(0,0,0);
    transform: translate3d(0,0,0);
}
```

## 移动端常规问题处理 
```css
li{  -webkit-tap-highlight-color:rgba(0,0,0,0) ; } /*阻止在ios(iphone和ipad)上长按可点击元素时，出现一个半透明的灰色背景。*/
img{-webkit-touch-callout:none; }/*当你触摸并按住触摸目标时候，禁止或显示系统默认菜单*/

/* html5+CSS 禁止IOS长按复制粘贴实现  */
*{
    -webkit-touch-callout:none;  /*系统默认菜单被禁用*/
    -webkit-user-select:none; /*webkit浏览器*/
    -khtml-user-select:none; /*早期浏览器*/
    -moz-user-select:none;/*火狐*/
    -ms-user-select:none; /*IE10*/
    user-select:none;
}
input,textarea {
    -webkit-user-select:auto; /*webkit浏览器*/
    outline: none;
}
select {
    -webkit-appearance: none; /*常用于IOS下移除原生样式*/
    -moz-appearance: none;
}
p {-webkit-filter: blur(1px);}  /*可模糊文字*/
```
## 文字两行一行显示 溢出省略号
```css
p{
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 2; /*设置显示行数*/
    overflow: hidden;
    font-size: 14px;
}
```
## input框placeholder颜色重置
```css
input::-webkit-input-placeholder { /* WebKit browsers */
    color:#45deb8;
}
input:-moz-placeholder { /* Mozilla Firefox 4 to 18 */
    color: #45deb8;
}
input::-moz-placeholder { /* Mozilla Firefox 19+ */
    color:#45deb8;
}
input:-ms-input-placeholder { /* Internet Explorer 10+ */
    color:#45deb8;
}
```
## 重置默认滚动条样式
```css
::-webkit-scrollbar{ display:none;}  /* 设置滚动条不显示  隐藏滚动条*/
::-webkit-scrollbar {/*滚动条整体样式*/
    width: 8px;     /*高宽分别对应横竖滚动条的尺寸*/
    height: 8px;
}
::-webkit-scrollbar-thumb {/*滚动条里面小方块*/
    border-radius: 10px;
    -webkit-box-shadow: inset 0 0 5px rgba(0,0,0,0.2);
    background: #ccc;
}
::-webkit-scrollbar-track {
    -webkit-box-shadow: inset 0 0 5px rgba(0,0,0,0.2);
    border-radius: 10px;
    background: #eee;
}
```
## cover / contain 的不同之处
```
// background-size : cover / contain 的不同之处
cover: 图片宽高比不变、铺满整个容器的宽高，而图片多出的部分则会被截掉
contain: 图片自身的宽高比不变，缩放至图片自身能完全显示出来，所以容器会有留白区域；
```
## rem文字自适应
```js的方式
(function (doc, win) {
	var docEl = doc.documentElement,
		resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
		recalc = function () {

			var clientWidth = docEl.clientWidth;
			if (!clientWidth) return;
			if (clientWidth >= 750) {
				docEl.style.fontSize = '100px';
			} else {
				docEl.style.fontSize = 100 * (clientWidth / 750) + 'px';
			}
		};

	if (!doc.addEventListener) return;
	win.addEventListener(resizeEvt, recalc, false);
	recalc()
	// doc.addEventListener('DOMContentLoaded', recalc, false);
	/*DOMContentLoaded文档加载完成不包含图片资源 onload包含图片资源*/
})(document, window);
```
```css
@media only screen and (max-width: 365px) {
    :root,html,body {font-size: 12px;}
}
@media only screen and (min-width: 365px) and (max-width: 410px) {
    :root,html,body {font-size: 14px; }
}
@media only screen and (min-width: 410px){
    :root,html, body {font-size: 16px;}
}
@media only screen and (min-width: 760px){
    :root,html,body {font-size: 28px;}
}
```