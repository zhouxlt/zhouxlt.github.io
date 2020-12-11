---
title: Github Pages + Hexo 搭建个人博客
---
参考：https://juejin.cn/post/6844904131266609165；https://zhuanlan.zhihu.com/p/35668237
github.io是每个Github账号可以免费拥有的一个域名，这个域名上部署的页面，称之为Github Pages，用户有高度自主权去DIY自己的“个人网站”。
通常，用户会将其用来作为自己的博客网站，存放一些博客、收藏、简历等，业界比较成熟的个人博客网站模板是Hexo，它基于Node.js，能快速生成一套可运行成博客页面的代码，用户将自己的文章加入并配置好相关信息，然后编译，推送到github.io仓库中，Github会自动将页面部署到服务器。不仅如此，Hexo上提供丰富多样的模板主题，可供选择。
# Github Pages + Hexo 搭建个人博客
## 准备
git、GitHub和nodejs
## Github Pages
### 创建Github Pages
配置好git和GitHub后，需要在GitHub上创建Github Pages服务
![Github Page创建](github-page.png "Github Page")
GitHub可以配置下SSH连接公钥
## 安装Hexo并初始化博客
### 安装Hexo及验证
``` bash
$ npm install -g hexo-cli
$ hexo -v
```
### 初始化项目
``` bash
$ hexo init {name}
```
| hexo命令 | 简写 | 说明 | 详述 |
| :---:| :---: | :---: |:---: |
|hexo clean| hexo c|清除本地缓存|清除public/文件夹和db.json文件|
|hexo generate| hexo g |编译|将souce下的Markdown和HTML文件解析到了public下，并生成了db.json文件|
|hexo serve|hexo s|本地运行|开启本地调试模式|
|hexo deploy|hexo d|部署|将本地资源部署到GithubPages|
|hexo new [layout] {title}||新建博客（文件夹及md文件）|一般忽略layout可选参数，默认为scaffolds模板的post|
|hexo help||查询hexo命令|

### hexo deply部署
#### 安装插件hexo-deployer-git
``` bash
$ npm install -S hexo-deployer-git
```
#### _config.yml中配置部署地址
``` yaml
deploy:
  type: git
  repo: git@github.com:yourname/yourname.github.io.git
  branch: main
```
#### 运行部署命令
``` bash
$ hexo deploy
```
#### 访问https://{username}.github.io/
可以看到在本地生成的博客已经可以在互联网上访问到了
做到这步已经可以了，但是需要通过翻墙才能访问到该网址
可以配置我们自己的个性域名，购买一个域名，做域名的解析配置；打开github博客项目，点击settings，拉到下面Custom domain处，填上你自己的域名，保存，就能使用个性域名访问啦
# Hexo生成站点目录结构
![hexo站点目录结构](hexo站点结构.png "hexo站点目录结构")
node_modules文件夹是执行npm install或yarn install，根据package.json文件安装的依赖插件
public文件夹和db.json文件，是执行了hexo generate命令之后，将souce文件夹下的Markdown和HTML文件解析到了public文件夹下，并生成了db.json文件

## scaffolds模板
使用不同的模板会创建到source下不同类型文件夹下
``` bash
$ hexo new [layout] {title}
```
| 布局 | 路径 | 说明 |
| :---:| :---: | :---: |
| post | source/_post | 默认 |
| page | source/ |
| draft | source/_draft |
## source资源
source资源文件夹，是存放用户资源的地方。
除post文件夹外，开头以_（下划线）命名的文件/文件夹或隐藏文件都会在generate时被忽略。Markdown和HTML文件夹会被解析到public文件夹下，其它文件格式的文件会被直接拷贝过去。
hexo new {title}创建博客时会在source文件夹下多一个文件夹和一个.md文件，一个用来存放你的图片等数据，另一个就是你的文章文件
## themes主题
下载的主题放在themes文件夹下，hexo默认的主题是landscape
## _config.yml配置文件
_config.yml是整个博客的配置文件，至于每项配置参数可以[Hexo官网文档](https://hexo.io/zh-cn/docs/configuration)有详细的介绍
# Hexo主题配置
在themes文件夹内新增一个以theme名称命名的文件夹，
根目录下的_config.yml博客配置文件中的theme字段中修改成对应的theme名称即可切换主题。
## 选择喜欢的hexo主题
在[Hexo主题网站](https://hexo.io/themes/)中选择喜欢的博客主题
## clone主题代码到themes/themeName
``` bash
$ cd root-path
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```
## _config.yml配置修改主题名字
``` yaml
theme: {themeName}
```
## 重新编译可以看到新的主题应用到博客
``` bash
$ hexo c
$ hexo g
$ hexo s
```
# git除了存储生成的静态页面，还要存放hexo开发代码
本地和发布分支
一个分支用来存放Hexo生成的网站原始的文件，另一个分支用来存放生成的静态网页
## 从hexo分支下载后的代码部署方式
### npm安装packge.json依赖到node_modules
``` bash
$ npm install
```
### hexo 编译
``` bash
$ hexo g
```
### hexo 部署到github page域名
``` bash
$ hexo d
```
# zhouxlt.github.io访问不了
## ping域名，看到了ip
``` bash
$ ping zhouxlt.github.io
```
![ping zhouxlt.github.io结果图](ping域名结果图.png "ping域名")
## 以太网Internet4协议配置
![配置DNS服务器](以太网配置Internet4DNS服务器.png "配置DNS服务器")
## 监测网络中DNS服务器是否能正确实现域名解析
![监测域名解析](域名解析.png "监测域名解析")
## 刷新DNS缓存
![刷新DNS缓存](刷新DNS缓存.png "刷新DNS缓存")
## 翻墙！！
一顿操作~~~结果是因为要翻墙~~~
