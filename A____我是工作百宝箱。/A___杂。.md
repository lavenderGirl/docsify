

#### 贝瑞小程序
- template模板使用
```html 
<!-- wxml页面中使用 -->
<import src="../compents/authorization/index.wxml" />
<template is="consumer" wx:if="{{consumer}}" data="{{speak}}"></template>
```

- wxs文件 写入一些公用方法
```html
<!-- wxml引用  -->
<!-- WXS 代码可以编写在 wxml 文件中的 <wxs> 标签内，或以 .wxs 为后缀名的文件内, 用module中的tools去访问common.wxs中的方法。例如：tools.gopay() -->
<wxs src="../../../wxs/common.wxs" module="tools"></wxs>
```

#### 小程序转uniapp

- mac的快捷键为: command+option+c   复制文件夹地址
- command+v 粘贴路径
- wtu -i /Users/sensen/Documents/FeiMaProject/BerryCoffee



#### javascript
- 字节跳动
    - JavaScript常用的API
    - react全家桶 | TypeScript | Node.js

#### 小程序文档学习


#### 面试题
- [Vue面试中，经常会被问到的面试题/Vue知识点整理](https://segmentfault.com/a/1190000016344599)
- [2020年前端面试复习必读文章【超百篇文章/赠复习导图】](https://juejin.im/post/5e8b163ff265da47ee3f54a6)




#### 美白
防晒到位、休息到位、饮食到位
- 关于吃 
    - [怎样内养祛黄美白?](https://www.zhihu.com/question/357806993/answer/1349070010)
    - [如何养成一张干净的脸](https://www.zhihu.com/question/34546303/answer/1044328804)



## 周会探讨

- 这两周要做的事情
- 团队中存在的问题
- 如何提升自我能力
- 怎样让周会时间更有意义

### 双周计划

这两周做什么，如果暂无项目可做的时候，是不是可以提前预知接下来要做项目的方向，这样可以利用平时的时间先学起来。

比如前端，现在地推宝要做的单页面项目，其实我之前是没有做过的，像整个框架用到的技术，怎么配置才能符合我们当前的业务逻辑，其实对于我个人而言都是要提前去学的。
[vue单页面后台管理实例](https://panjiachen.gitee.io/vue-element-admin-site/zh/guide/#功能)
。

再比如设计，我相信豪弟的能力，什么都可以做，一个项目可能两天就做完了，其他时间我们是不是可以想想为这个团队做点什么，比如图标，后台页面里做了很多页面，也用到了很多图标，是不是可以做一个整合等。

其次，小马哥有时间也可以给我们讲讲项目的业务逻辑。很多时候只是看葫芦画瓢，看着设计做页面，做完了也不知道这个页面是干什么的。


### 团队中存在的问题

设计、前端、后端没有形成一个闭环，有时候会出现，前端这边做好了，后端可能还不知道界面是什么。【暂时想到的解决办法：做项目时，涉及到的资源修改都邮件抄送相关人员，这样大家都知道】


### 如何提升自我能力

当我们能好好的完成当下的任务的时候，其实是很容易固步自封的。

就我个人来说【1、写文章累积，2、跟以前的朋友聊聊，3、看看gitHub，[哔哩哔哩](https://space.bilibili.com/433498120/favlist?fid=469838220&ftype=create)等】


### 怎样让周会时间更有意义 

分享你认为值得分享的所有东西

比如：[看复旦大学陈果谈自信、谈幸福、谈优雅、谈生活乐趣](https://space.bilibili.com/433498120/favlist?fid=495165020&ftype=create)


### uniapp
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

- [vuex：弄懂mapState、mapGetters、mapMutations、mapActions](https://zhuanlan.zhihu.com/p/100941659)


