##### [为什么clear:both不起作用？](https://developer.mozilla.org/en-US/docs/Web/CSS/clear)
- clear属性只是在block元素是起作用

##### 2019-05-05
- 修改地图颜色
- 爬虫页面360浏览器不显示等兼容性问题
- 爬虫页面改版 完成80%

2019-05-05日报：
1.地图配色
2.爬虫页面360兼容性问题修复
3.爬虫页面改版 完成70%

2019-05-06日报：
1.大宗商品页面兼容性处理
2.生猪页面全新改版。

2019-05-07日报：
1.大宗商品页面优化
2.期货相关页面随接口变化调整布局。

2019-05-08日报：
1.大宗商品-自定义弹框优化
2.大宗商品-地图颜色根据数据动态显示，优化地图在某个区间显示为一个色的情况
3.大宗商品-添加引导页

2019-05-09日报：
1.大宗商品-引导页与地图再优化，并同步所有大宗商品页面。
2.开会问题记录的相关优化。
##### 2019-05-09要修复问题
- 地区价格：tip (数据红是平，红涨绿跌)
- 走势图：加单位 例如猪价(元)
- 鸡蛋页面：去掉玉米、豆粕
- 时间维度 根据数据显示 数据为本周就显示本周
- 地图：lenged 竖轴
- 期货页面：时间要是最新  数字加单位 数字千分位  左轴间距遮住问题(左轴浮在左边里面)
- 折线与期货图最后一天要明显显示
- 地区价格 + 全国
- 引导页控制-调用接口

##### 2019-05-13 大宗商品修复 & 点评信息页面前端开发
- 根据日期显示有数据的日期
- 日期选择不够明显
- 折线图底色
- map文字重叠在一起的情况
- 点评信息-品牌&门店选择、店面比较静态界面开发完

##### 2019-05-14 点评信息页面前端开发
- 口味对比
- 店面词云
- 评论
- TOP产品


##### 点评信息页面(工时：31/8 == 3.8天)(前端开发+接口对接+联调+测试优化)
- 1.品牌&门店选择 1day 
- 2.店面比较 1day
- 3.口味对比 1.5day
- 4.店面词云 2day
- 5.评论 5h
- 6.TOP产品 5h
- 7.TOP门店 1h
- 8.上新时间表 5h

##### 点评数据页面(工时:26/8 = 3天)
- 1.品牌&门店选择 3h
- 2.基础信息 2h
- 3.用户评价 5h
- 4.评价词云 2h
- 5.TOP产品 4h
- 6.TOP门店 1h
- 7.上新时间表 5h
- 8.新品词云 2h
- 9.评价趋势 2h

##### 2019-05-24工作记录
- 1.选择第一个门店时，会弹出"请先选择门店提示框"
- 2.删除一个门店再点查询时，删除的门店的店铺词云还在
- 3.评论模块-同一个地区不同品牌只显示一个地区模块的问题处理
- 4.TOP产品模块，不同品牌下分成两列,数值千分位显示
- 5.TOP门店添加排名一列
- 6.上新时间表一进页面默认应有高度显示loading，当有数据时去除高度自适应。
- 7.口味对比模块雷达图无法显示问题

##### 2019-05-27工作记录
- 1.点评门店&点评对比页面代码优化整理
- 2.店铺词云整体优化。
- 3.食安点评页面开发。

##### 2019-05-28工作记录
- 1.点评门店增加评论最早最晚时间
- 2.单店时TOP门店不要，重新排版布局。
- 3.TOP产品增加占比
- 4.TOP门店增加店龄

##### 2019-05-29工作记录
- 门店对比页面TOP产品添加占比，Top门店店龄格式化为以年为单位
- 点评门店、点评对比页面上新时间模块flex跟日期在360里的兼容性问题处理
- 食安点评查询条件改变
- 大宗商品(鸡苗、鸭苗页面把"元/公斤"改成"元/羽";毛鸡、毛鸭页面把"元/公斤"改成"元/斤")
- 食安跟真臻鲜点评接口区分修改。

##### 2019-05-30工作记录
- 1.真臻鲜点评与食安点评四个页面整体优化。
- 1.口味对比模块标题遮住图
- 2.对比页面-TOP产品品牌过多时，有些列显示不全问题
- 3.查询条件选中项底色添加
- 4.店面比较饼图文字过长遮住修复


##### 2019-05-31
- npm、node.js
- npm install -g cnpm --registry=https://registry.npm.taobao.org 全局安装cnpm
- cnpm install webpack -g
- cnpm webpack-cli
- npm run start 
    - vue
    - axios
    - babel-polyfill
    - echarts
    - element-ui
    - font-awesome
    
##### 2019-06-03
- 大宗商品跟真臻鲜点评、食安点评页面接口统一规范
- webpack项目构建研究

##### 2019-06-04
- 智能引擎页面开发
- webpack项目尝试搭建学习

##### 2019-06-05博客可以记录一些什么
- 前端工程化需要学习哪些技术
- 如何构建一个多页面或者单页面项目
- 规范化
- “哔哩哔哩”前端技术学习

- 智能引擎页面调整优化
- xData系统首页移动端自适应优化

- webpack配置中很多用到的是node.js中的语法
- [多页面webpack配置时是否需要new HtmlWebpackPlugin多个](https://segmentfault.com/q/1010000016741903)
- [glob在webpack中的使用](https://www.cnblogs.com/waitforyou/p/7044171.html)

##### 2019-06-06 [webpack4](https://www.cnblogs.com/cangqinglang/p/8964460.html)
- 安装npm、node.js
- npm install -g cnpm --registry=https://registry.npm.taobao.org 全局安装cnpm 
- cnpm init  【生成package.json】
- cnpm i webpack webpack-cli -D 或者 cnpm install webpack weback-cli --save-dev 【npm i -D是cnpm install --save-dev的简写，是指安装模块并保存到package.json的devDependencies中，主要在开发环境中的依赖包】

- 涉及到的点：npx(npm是node自带的，npm从5.2版开始，增加了npx) nvm


- plugins (例如：npm i webpack-dev-server -D)
    - webpack-dev-server【启动devServer需要安装一下webpack-dev-server】
    - [html-webpack-plugin](https://www.cnblogs.com/wonyun/p/6030090.html)
    - style-loader css-loader 
    - extract-text-webpack-plugin 【功效就在于会将打包到js里的css文件进行一个拆分】
    - file-loader url-loader 【引用图片需要用到的loader】
    - html-withimg-loader【img引用的图片地址】
    - postcss-loader autoprefixer 【添加CSS3前缀】
    - babel-core babel-loader babel-preset-env babel-preset-stage-0 【转义ES6】
    - clean-webpack-plugin 【每次打包之前将dist目录下的文件都清空】
    
    - html-webpack-inline-source-plugin
    - mini-css-extract-plugin
    - optimize-css-assets-webpack-plugin
    - uglifyjs-webpack-plugin

##### 2019-06-10
- 以点评项目为例进行webpack4项目构建

##### 2019-06-11
- 以点评项目为例进行webpack4项目构建优化

##### 2019-06-12
- 智能引擎页面接口对接
- 构建目录结构优化

- 单页面webpack工程目录结构
- src
    - assets 全局资源目录
        - images 图片
        - less //less样式表
        - css //css样式表
        - fonts //自定义字体文件
    - components //公共组件目录
        - Slider.vue 
    - directives.js //公共指令
    - filters.js //公共过滤器
    - login
        - index.vue //入口文件
        - LoginForm.vue //登录场景私有表单组件
        - SocialLogin.vue
    - cart 
        - index.vue
        - ItemList.vue
    - Discover.vue //场景入口文件
    - App.vue //默认程序入口
    - main.js 
    
#### 2019-06-13
- less
- 共用css样式less化。
- webpack4构建项目中-真臻鲜与食安点评页面样式less修改 组件化修改

#### 2019-06-14
- 真臻鲜与食安点评页面组件化; 样式less; js脚本改成ES.js语法
- 接下来要做的事情：
    - dev环境与pro环境配置区分开来
    - 请求接口统一放在api.js文件中进行管理
    - 图片需要如何配置才能在js、html、css中引入使用

#### 2019-06-17
- dev环境与pro环境配置区分开来
- 请求接口统一放在api.js文件中进行管理

#### 2019-06-18
- 以项目为准 更改打包路径
- webpack构建项目本地启动在IE上运行报错的问题研究

#### 2019-06-19 [打包配置参考](https://github.com/lhy2813419591/webpackTemplate)
- 为何构建项目时  删除不了dist文件夹里的文件？已修复
- webpack项目配置文件拆分为dev跟prod文件

#### 2019-06-20
- 本地json文件如何在页面中使用
- 大宗商品迁移到webpack项目中去

#### 2019-06-21
- 大宗商品-期货页面迁移[棕榈油、大豆油、糖]
- 样式不能跨页面应用...

#### 2019-06-24
- 大宗商品页面样式less格式化 
- 各页面迁移到webpack项目中后数据对比 看是否有错
- 大宗商品-价格走势图最低值与横坐标的间距调整。

#### 2019-06-25
- 推荐引擎页面迁移
- ES6语法修改js脚本，less修改css
- 各页面样式less化之后提取公共样式

#### 2019-06-26
- 法律法规+新闻页面迁移
- 大宗商品各页面优化

#### 2019-06-27
- xdata项目添加目录文件
- 舆情页面-法律法规接口对接

#### 2019-06-28
- 舆情页面接口数据对接，以及页面布局优化，公共样式提取。

#### 2019-07-01
- 舆情-法律法规与新闻页面接口对接。

#### 2019-07-02
- 舆情 页面样式优化以及页面迁移到webpack项目中，各页面脚本ES6语法修改与样式Less化等


#### 2019-07-03
- 点评页面柱状图滚动条随着数据缩放优化(Q:数据量大时全粘一块了)
- 舆情-法规页面新增模块数据对接。

#### 2019-07-04
- 舆情数据有误核对、详情页状态不同显示天数计算等。
- xdata首页添加导览。

#### 2019-07-05
- 舆情页面测试再优化
- xdata首页图标替换，导览再优化。
- 项目性能优化研究

#### 2019-07-08
- xdata项目性能优化
- 首页导览优化

#### 2019-07-09
- xdata项目构建优化
    - 减少编译体积大小
    - 将大型库外链
    - 将库预先编译
    - 使用缓存
    - 并行编译
- 智能推荐页面调试修改

#### 2019-07-10
- 首页图标跟导览文字修改
- xdata项目打包之每次hash值不要全变，只变修改的内容
- DMP几个页面迁移

#### 2019-07-11
- DMP在xdata跑通以及优化css跟js
- 测试xdata在其他浏览器显示的兼容性问题
- 首页迁移以及原先的jquery实现交互改成vue,减少引入多类型库

#### 2019-07-12
- 首页导览改变布局跟交互从而修复每一页都显示箭头。
- 《编写高质量代码-web前端开发修炼之道》阅读-179页

#### 2019-07-15
- xdata错误信息进行统一处理
- dmp页面优化
- 小程序学习

#### 2019-07-16
- xdata项目在IE兼容性问题处理
- 百度地图研究
- 后台管理系统权限管理研究

#### 2019-07-17
- 百度地图demo
- 首页导览跟登录退出按钮接口控制
```
toolbox: {
    show: true,
    feature: {
        // dataZoom: {
        //     yAxisIndex: 'none'
        // },
        dataView: {
            title:'数据视图',
            lang:['数据视图', '关闭', '刷新']
        },
        // magicType: {type: ['line', 'bar']},
        // restore: {},
        saveAsImage: {title:'保存为图'}
    }
},
```

#### 2019-07-18
- xdata项目打包图片路径问题研究
- 推荐引擎页面门店数据对接

#### 2019-07-19
- 推荐引擎页面 柱状图点击改变排名开发

#### 2019-07-12 ~ 2019-07-19
主要任务：
- 首页导览修复每一页都带左右箭头的问题
- 首页导览跟登录退出按钮通过接口控制是否显示
- xdata错误信息进行统一处理
- xdata在IE兼容性问题修复 
- xdata打包图片路径问题研究
- 推荐引擎页面门店数据对接