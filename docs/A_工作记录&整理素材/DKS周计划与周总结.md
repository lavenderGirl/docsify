[不要告诉我你懂margin](http://www.hicss.net/do-not-tell-me-you-understand-margin/)

#### 本周要做的事情(2019-7-29 ~ 2019-8-2)
- qscv页面数据对接 
- 整一个单页面项目
- 把人机对话、人脸识别、考勤打卡放到里面去

#### 本周任务(2019-8-19 ~  2019-8-23)

```
扫码购小程序：
账户：hairongzheng@x2era.com
密码：Abc@123456

AppID：wxf448f02b12ef8229
AppSecret：6404fba90d3cf0f0b97d8d9e845a9db9

```
- 小程序 - 扫码购
    - 注册登录【微信授权获取手机号、如何请求接口、公用数据存储、页面跳转】
        - 注册登录接口1个
        - 用户状态1个(已认证、未认证状态，已核销未核销状态)
    - 拍照认证【1.未认证：拍照认证; 2.已认证：跳首页 ————知识点：上传照片认证】
    - 商品核销 【可能显示信息：微信头像、订单信息、二维码】
    - 个人中心-认证
    - 个人中心-历史订单
    - 大屏核销H5 

- 数据存储
```
wx.getStorageSync('gltoken')
```

- 请求接口

- 显示提示框
```
//index.js已经封装
const showToast = function(str) {
  wx.showToast({
    title: str,
    icon: "none",
    duration: 1500
  })
}
//页面用的时候：
import util from "../../../utils/index"
util.showToast('请选择渠道！')
```

- 跳转页面——wx.redirectTo (关闭当前页面，跳转到应用内的某个页面。但是不允许跳转到 tabbar 页面。)
```
wx.redirectTo({ url: "/pages/login/login" });
```

- 上传图片：wx.uploadFile
```
//从本地相册选择图片或使用相机拍照。
wx.chooseImage({
  success (res) {
    const tempFilePaths = res.tempFilePaths
    wx.uploadFile({
      //仅为示例，非真实的接口地址
      url: 'https://example.weixin.qq.com/upload', 
      filePath: tempFilePaths[0],
      name: 'file',
      formData: {
        'user': 'test'
      },
      success (res){
        const data = res.data
        //do something
      }
    })
  }
})

```

- 更新机制
```
//放在了app.js的onLaunch方法里了,发布的第一版不会生效，下一版才会生效的
// 获取小程序更新机制兼容
//wx.canIUse 判断小程序的API，回调，参数，组件等是否在当前版本可用
if (wx.canIUse('getUpdateManager')) {
    const updateManager = wx.getUpdateManager()
    updateManager.onCheckForUpdate(function (res) {
    // 请求完新版本信息的回调
    if (res.hasUpdate) {
        updateManager.onUpdateReady(function () {
        wx.showModal({
            title: '更新提示',
            content: '新版本已经准备好，是否重启应用？',
            success: function (res) {
            if (res.confirm) {
                // 新的版本已经下载好，调用 applyUpdate 应用新版本并重启
                updateManager.applyUpdate()
            }
            }
        })
        })
        updateManager.onUpdateFailed(function () {
        // 新的版本下载失败
        wx.showModal({
            title: '已经有新版本了哟~',
            content: '新版本已经上线啦~，请您删除当前小程序，重新搜索打开哟~',
        })
        })
    }
    })
} else {
    // 如果希望用户在最新版本的客户端上体验您的小程序，可以这样子提示
    wx.showModal({
    title: '提示',
    content: '当前微信版本过低，无法使用该功能，请升级到最新微信版本后重试。'
    })
}
```

- 直接获取微信头像

```
<open-data type="groupName" open-gid="xxxxxx"></open-data>
<open-data type="userAvatarUrl"></open-data>
<open-data type="userGender" lang="zh_CN"></open-data>
```

- 微信扫一扫功能
```
wx.scanCode({
  success: (res) => {
    console.log(res)
  }
})
```



### 小程序学习
- 小程序后台管理[需要账号]
    - 小程序名称【发布前可修改2次】、小程序简称【一年内可修改2次】、小程序头像【一年内可申请修改5次】、小程序介绍【一个月可申请5次】、服务类目【一个月可申请3次】

- 微信小程序App()方法与getApp()方法
  - App()：注册一个小程序、小程序的入口方法【必须在app.js 中注册，且不能注册多个】
    ```javascript
    //app.js中
    App({
      globalData: {
        userInfo:null,
        helloFromApp:'Hello,I am From App.js'
      }
    })
    ```
  - getApp()：通过getApp获取全局对象，然后进行全局变量和全局方法的使用

    ```javascript
    // 其他页面中想调用全局变量和方法时
    var app = getApp();
    console.log(app.globalData.helloFromApp); // 调用全局变量
    app.test(); 
    ```
- 微信小程序生命周期【onLoad有Object query参数，在onLoad 的参数中获取打开当前页面路径中的参数】
