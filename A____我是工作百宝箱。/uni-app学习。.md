- [ccm-b2b2c-uniapp](https://gitee.com/luochangqing/ccm-b2b2c-uniapp)

- 条件编译 
```js
// 如下代码只会编译到H5的发行包里，其他平台的包不会包含如上代码
// #ifdef H5
    alert("只有h5平台才有alert方法")
// #endif


// 可使用 uni.getSystemInfoSync().platform 判断客户端环境是 Android、iOS 还是小程序开发工具（在百度小程序开发工具、微信小程序开发工具、支付宝小程序开发工具中使用 uni.getSystemInfoSync().platform 返回值均为 devtools)
switch(uni.getSystemInfoSync().platform){
    case 'android':
       console.log('运行Android上')
       break;
    case 'ios':
       console.log('运行iOS上')
       break;
    default:
       console.log('运行在开发者工具上')
       break;
}
```
    - 条件编译是利用注释实现的，在不同语法里注释写法不一样，js使用 // 注释、css 使用 /* 注释 */、vue/nvue 模板里使用 <!-- 注释 -->

- 个性的代码放到不同平台的目录下，差异化维护