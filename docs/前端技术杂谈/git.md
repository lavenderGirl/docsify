# Git 

一般来说，日常使用只要记住下图6个命令，就可以了。但是熟练使用，恐怕要记住60～100个命令。
![](https://i.loli.net/2018/11/20/5bf3d93442601.png)
下面是常用 Git 命令清单。几个专用名词的译名如下。
```
Workspace：工作区
Index / Stage：暂存区
Repository：仓库区（或本地仓库）
Remote：远程仓库
```
#### 一、新建代码库
```
# 在当前目录新建一个Git代码库
$ git init

# 新建一个目录，将其初始化为Git代码库
$ git init [project-name]

# 下载一个项目和它的整个代码历史
$ git clone [url]

# 拉取线上develop分支的代码
$ git clone -b develop git@gitee.com:php_martin/dtb.git

```
#### 二、配置
Git的设置文件为.gitconfig，它可以在用户主目录下（全局配置），也可以在项目目录下（项目配置）。
```
# 显示当前的Git配置
$ git config --list

# 编辑Git配置文件
$ git config -e [--global]

# 设置提交代码时的用户信息
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]"
```
#### 三、增加/删除文件
```
# 添加指定文件到暂存区
$ git add [file1] [file2] ...

# 添加指定目录到暂存区，包括子目录
$ git add [dir]

# 添加当前目录的所有文件到暂存区
$ git add .

# 添加每个变化前，都会要求确认
# 对于同一个文件的多处变化，可以实现分次提交
$ git add -p

# 删除工作区文件，并且将这次删除放入暂存区
$ git rm [file1] [file2] ...

# 停止追踪指定文件，但该文件会保留在工作区
$ git rm --cached [file]

# 改名文件，并且将这个改名放入暂存区
$ git mv [file-original] [file-renamed]
```
#### 四、代码提交
```
# 提交暂存区到仓库区
$ git commit -m [message]

# 提交暂存区的指定文件到仓库区
$ git commit [file1] [file2] ... -m [message]

# 提交工作区自上次commit之后的变化，直接到仓库区
$ git commit -a

# 提交时显示所有diff信息
$ git commit -v

# 使用一次新的commit，替代上一次提交
# 如果代码没有任何新变化，则用来改写上一次commit的提交信息
$ git commit --amend -m [message]

# 重做上一次commit，并包括指定文件的新变化
$ git commit --amend [file1] [file2] ...
```
#### 五、分支
```
# 列出所有本地分支
$ git branch

# 列出所有远程分支
$ git branch -r

# 列出所有本地分支和远程分支
$ git branch -a

# 新建一个分支，但依然停留在当前分支
$ git branch [branch-name]

# 新建一个分支，并切换到该分支
$ git checkout -b [branch]

# 新建一个分支，指向指定commit
$ git branch [branch] [commit]

# 新建一个分支，与指定的远程分支建立追踪关系
$ git branch --track [branch] [remote-branch]

# 切换到指定分支，并更新工作区
$ git checkout [branch-name]

# 切换到上一个分支
$ git checkout -

# 建立追踪关系，在现有分支与指定的远程分支之间
$ git branch --set-upstream [branch] [remote-branch]

# 合并指定分支到当前分支
$ git merge [branch]

# 选择一个commit，合并进当前分支
$ git cherry-pick [commit]

# 删除分支
$ git branch -d [branch-name]

# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
```
#### 六、标签
```
# 列出所有tag
$ git tag

# 新建一个tag在当前commit
$ git tag [tag]

# 新建一个tag在指定commit
$ git tag [tag] [commit]

# 删除本地tag
$ git tag -d [tag]

# 删除远程tag
$ git push origin :refs/tags/[tagName]

# 查看tag信息
$ git show [tag]

# 提交指定tag
$ git push [remote] [tag]

# 提交所有tag
$ git push [remote] --tags

# 新建一个分支，指向某个tag
$ git checkout -b [branch] [tag]
```
#### 七、查看信息
```
# 显示有变更的文件
$ git status

# 显示当前分支的版本历史
$ git log

# 显示commit历史，以及每次commit发生变更的文件
$ git log --stat

# 搜索提交历史，根据关键词
$ git log -S [keyword]

# 显示某个commit之后的所有变动，每个commit占据一行
$ git log [tag] HEAD --pretty=format:%s

# 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
$ git log [tag] HEAD --grep feature

# 显示某个文件的版本历史，包括文件改名
$ git log --follow [file]
$ git whatchanged [file]

# 显示指定文件相关的每一次diff
$ git log -p [file]

# 显示过去5次提交
$ git log -5 --pretty --oneline

# 显示所有提交过的用户，按提交次数排序
$ git shortlog -sn

# 显示指定文件是什么人在什么时间修改过
$ git blame [file]

# 显示暂存区和工作区的代码差异
$ git diff

# 显示暂存区和上一个commit的差异
$ git diff --cached [file]

# 显示工作区与当前分支最新commit之间的差异
$ git diff HEAD

# 显示两次提交之间的差异
$ git diff [first-branch]...[second-branch]

# 显示今天你写了多少行代码
$ git diff --shortstat "@{0 day ago}"

# 显示某次提交的元数据和内容变化
$ git show [commit]

# 显示某次提交发生变化的文件
$ git show --name-only [commit]

# 显示某次提交时，某个文件的内容
$ git show [commit]:[filename]

# 显示当前分支的最近几次提交
$ git reflog

# 从本地master拉取代码更新当前分支：branch 一般为master
$ git rebase [branch]
```
#### 八、远程同步
```
$ git remote update  --更新远程仓储
# 下载远程仓库的所有变动
$ git fetch [remote]

# 显示所有远程仓库
$ git remote -v

# 显示某个远程仓库的信息
$ git remote show [remote]

# 增加一个新的远程仓库，并命名
$ git remote add [shortname] [url]

# 取回远程仓库的变化，并与本地分支合并
$ git pull [remote] [branch]

# 上传本地指定分支到远程仓库
$ git push [remote] [branch]

# 强行推送当前分支到远程仓库，即使有冲突
$ git push [remote] --force

# 推送所有分支到远程仓库
$ git push [remote] --all
```
#### 九、撤销
```
# 恢复暂存区的指定文件到工作区
$ git checkout [file]

# 恢复某个commit的指定文件到暂存区和工作区
$ git checkout [commit] [file]

# 恢复暂存区的所有文件到工作区
$ git checkout .

# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
$ git reset [file]

# 重置暂存区与工作区，与上一次commit保持一致
$ git reset --hard

# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
$ git reset [commit]

# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
$ git reset --hard [commit]

# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
$ git reset --keep [commit]

# 新建一个commit，用来撤销指定commit
# 后者的所有变化都将被前者抵消，并且应用到当前分支
$ git revert [commit]

# 暂时将未提交的变化移除，稍后再移入
$ git stash
$ git stash pop
```
#### 十、其他
```
# 生成一个可供发布的压缩包
$ git archive
```
git原文章地址：[https://www.cnblogs.com/chenwolong/p/GIT.html](https://www.cnblogs.com/chenwolong/p/GIT.html)

# 特殊处理-回滚
```
  - git reset --hard [commit-hash:e377f60e28c8b84158]
  - git push -f origin [branch]
```

# Git Flow代码示例
#### a.创建develop分支
```
# 新建develop分支
git branch develop 

# 与远程develop分支建立追踪关系 -u之后，后面push时直接git push即可
git push -u origin develop
```
#### b.开始新Feature开发
```
# 以develop为基础创建some-feature分支，并切换到该分支
git checkout -b some-feature develop 

<!-- Optionally,push branch to origin: -->
<!-- git push -u origin some-feature -->

# 做一些改动
git status
git add some-file
git commit
```
#### c.完成Feature
```
git pull origin develop
git checkout develop
git merge --no-ff some-feature
git push origin develop

# 删除分支some-feature
git branch -d some-feature

<!--  if you pushed branch to origin: -->
git push origin --delete some-feature

```
#### d.开始relase
```
git checkout -b release-0.1.0 develop

<!-- optional:Bump version number,commit -->
<!-- Prepare release,commit -->
```

#### e.完成release
```
git checkout master
git merge --no-ff release-0.1.0
git push 

git checkout develop
git merge --no-ff release-0.1.0
git push

git branch -d release-0.1.0

<!-- if you pushed branch to origin -->
git push origin --delete release-0.1.0

git tag -a v0.1.0 master
git push --tags
```

#### f.开始Hotfix
```
git checkout -b hotfix-0.1.1 master
```

#### g.完成Hotfix
```
git checkout master
git merge --no-ff hotfix-0.1.1
git push

git branch -d hotfix-0.1.1

git tag -a v0.1.1 master
git push --tags
```

# 配置SSH
```
# 提前安装git 用git bash测试

# 检查本机是否有ssh key设置
$ cd ~/.ssh
# 如果没有则提示：No such file or directory
# 如果有则进入~/.ssh路径下(ls查看当前路径文件，rm * 删除所有文件)

# 使用git bash生成新的ssh key
# 保证当前路径在“~”下
$ cd ~ 

# 建议填写自己真实有效的邮箱地址，然后一路回车即可
$ ssh-keygen -t rsa -C "xxxxxx@yy.com"  

# 查看生成的公钥
$ cat ~/.ssh/id_rsa.pub
```

# webpack JS启用babel转码
```
# 首先安装
npm i -D babel-loader babel-core babel-preset-env

# 在webpack的配置文件中,添加js的处理模块
module:{
    rules:[
        //‘transform-runtime’ 插件告诉babel要引用runtime来代替注入
        {
            test:/\.js$/,
            exclude:/(node_modules)/,
            use:{
                loader:'babel-loader',
                options:{
                    cacheDirectory:true
                }
            }
        }
    ]
}

# .babelrc文件如下：
{
    "presets":["env"]
}

# 再安装
npm install babel-plugin-transform-runtime --save-dev
npm install babel-runtime --save

# 修改 .babelrc
{
    "presets":["env"],
    "plugins":[
        ["transform-runtime",{
            "helpers":true,
            "polyfill":true,
            "regenerator":true,
            "moduleName":"babel-runtime"
        }]
    ]
}

# 安装babel-polyfill，然后再import 'babel-polyfill'使支持promise
install --save-dev babel-polyfill
```

# package.json
```
  --quiet 控制台中不输出打包的信息
  --compress 开启gzip压缩
  --progress 显示打包的进度
  
  "scripts": {
    "dev": "cross-env NODE_ENV=dev webpack-dev-server --quiet --config config/webpack.config.dev.js",
    "build": "cross-env NODE_ENV=prod webpack --config config/webpack.config.prod.js"
  },
```

# nodejs npm常用命令

npm是一个node包管理和分发工具，已经成为了非官方的发布node模块（包）的标准。有了npm，可以很快的找到特定服务要使用的包，进行下载、安装以及管理已经安装的包。
```
# 会引导你创建一个package.json文件，包括名称、版本、作者这些信息等
npm init

# 查看当前包的安装路径
npm root

# 查看全局的包的安装路径
npm root -g

# 查看npm安装的版本
npm -v

node的安装分为全局模式和本地模式。
一般情况下会以本地模式运行，包会被安装到和你的应用程序代码的本地node_modules目录下。
在全局模式下，Node包会被安装到Node的安装目录下的node_modules下。

# 安装Node模块,安装完毕后会产生一个node_modules目录，其目录下就是安装的各个node模块。
npm install moduleNames

# 默认会安装express的最新版本
npm install express 

# 安装指定版本
npm install express@3.0.6

# 将模块依赖关系写入到package.json文件的dependencies参数中
npm install <name> --save 

# 将模块依赖关系写入到package.json文件的devDependencies参数中
npm install <name> -dev 

# 全局安装,全局的安装是供命令行使用
npm install moduleName -g。

# 清除缓存
npm cache clean --force

# 验证缓存
npm cache verify

# 用淘宝npm镜像替换npm 
npm install -g cnpm --registry=https://registry.npm.taobao.org

# 查看node模块的package.json文件夹
npm view moduleNames

# 查看package.json文件夹下某个标签的内容
npm view moduleName labelName

# 查看当前目录下已安装的node包,Node模块搜索是从代码执行的当前目录开始的，搜索结果取决于当前使用的目录中的node_modules下的内容
npm list

# 查看帮助命令
npm help

# 模块信息（名称、版本号、依赖关系、Repo）例如：npm view jquery author
npm view <moudleName> [package.json属性名称]

# 查看包的依赖关系
npm view moudleName dependencies

# 查看包的源文件地址
npm view moduleName repository.url

# 查看包所依赖的Node的版本
npm view moduleName engines

# 查看npm使用的所有文件夹
npm help folders

# 用于更改包内容后进行重建
npm rebuild moduleName

# 检查包是否已经过时，此命令会列出所有已经过时的包，可以及时进行包的更新
npm outdated

# 更新node模块 npm update [<name><version>][-g]/[--save][-dev]
npm update moduleName 

# 卸载node模块 npm uninstall [<name><version>][-g]/[--save][-dev]
npm uninstall moudleName

# 一个npm包是包含了package.json的文件夹，package.json描述了这个文件夹的结构。访问npm的json文件夹的方法如下：
$ npm help json 

# 发布一个npm包的时候，需要检验某个包名是否已存在
$ npm search packageName

# npm模块发布,发布之前我们必须在NPM上有一个自己的账号
npm publish <name>

# npm账号注册，以邮箱方式
npm adduser

```
