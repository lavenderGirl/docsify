
### VSCode与Git，Git与Github。 
[【先去下载git】](https://git-scm.com/)[【Git 中文安装教程】](https://www.cnblogs.com/ximiaomiao/p/7140456.html)百度看了好多篇资料，发现[【Git工具详解以及与GitHub的配合使用】](https://www.cnblogs.com/Ant-soldier/p/6106777.html)这篇文章说的还是很详细的，毕竟我看下来，通过实际操作，虽说不上全通，至少从github上拉下来后，在vscode里修改后，再推送到github上是OK了。后续慢慢熟悉起来。[如何让github的项目能够访问的参考资料](http://www.cnblogs.com/wyhlightstar/p/6669936.html?utm_source=itdadao&utm_medium=referral)

[gitHub到底能做什么](https://github.com/phodal/github)

### 如何判断一个变量是否为数组（isArray）

1、instanceof

```
function isArray (obj) {
  return obj instanceof Array;
}
```
2、Array对象的 isArray方法
```
function isArray (obj) {
  return Array.isArray(obj);
}
```
3、Object.prototype.toString
```
function isArray (obj) {
  return Object.prototype.toString.call(obj) === '[object Array]';
}
```
- [两个行块宽度50%却不在同一行](https://segmentfault.com/q/1010000008603072)
- [vscode cssrem插件使用(px 自动转化成 rem)](https://www.jianshu.com/p/bb48fbdacb26)
- [在线px转rem](https://520ued.com/tools/rem)
- [模糊、阴影等效果图设置](http://www.css88.com/html5-demo/-webkit-filter/index.html)
- [修改IntelliJ IDEA里的内容后无需重启  浏览器同步的问题解决](https://www.cnblogs.com/kingxiaozi/p/6344432.html)
- input输入框禁止显示历史记录：添加属性 autocomplete="off" (注意：满足以下2个条件时，浏览器会自动记录输入过的值)
    - input标签在form标签下；点击了此form标签下的submit按钮;

>安装cssrem后。使用正常的px单位书写css后 按**ctrl+p** 再按**ctrl+r**可快速把px转换成rem单位。如果要设置font-size的值可以点击vscode左下角设置按钮点击设置之后找到cssrem进行设置即可。设置完成后重启即可生效。





### vue 项目构建
在node.js 以及npm安装的前提下。用vue-cli脚手架简单构建一个项目。
- $ npm install -g vue-cli
- $ vue init webpack my-project
- $ cd my-project
- $ npm install
- $ npm run dev

### [全局引入jquery](https://segmentfault.com/a/1190000007020623) 
1.  npm install jquery --save  成功之后会把jquery加入package.json的dependencies对象里。
2. 然后在需要的页面中引入就OK了     例如：import $ from 'jquery'
