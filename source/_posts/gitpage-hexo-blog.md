---
title: Github Pages + Hexo 搭建个人博客
---
github.io是每个Github账号可以免费拥有的一个域名，这个域名上部署的页面，称之为Github Pages，用户有高度自主权去DIY自己的“个人网站”。
通常，用户会将其用来作为自己的博客网站，存放一些博客、收藏、简历等，业界比较成熟的个人博客网站模板是Hexo，它基于Node.js，能快速生成一套可运行成博客页面的代码，用户将自己的文章加入并配置好相关信息，然后编译，推送到github.io仓库中，Github会自动将页面部署到服务器。不仅如此，Hexo上提供丰富多样的模板主题，可供选择。

## git除了存储生成的静态页面，还要存放hexo开发代码
本地和发布分支
一个分支用来存放Hexo生成的网站原始的文件，另一个分支用来存放生成的静态网页
### 从hexo分支下载后的代码部署方式：
#### npm安装packge.json依赖到node_modules
``` bash
$ npm install
```
#### hexo 编译
``` bash
$ hexo g
```
#### hexo 部署到github page域名
``` bash
$ hexo d
```
## zhouxlt.github.io访问不了
### ping域名，看到了ip
``` bash
$ ping zhouxlt.github.io
```
![ping zhouxlt.github.io结果图](ping域名结果图.png "ping域名")
### 以太网Internet4协议配置
![配置DNS服务器](以太网配置Internet4DNS服务器.png "配置DNS服务器")
### 监测网络中DNS服务器是否能正确实现域名解析
![监测域名解析](域名解析.png "监测域名解析")
### 刷新DNS缓存
![刷新DNS缓存](刷新DNS缓存.png "刷新DNS缓存")
### 翻墙！！
一顿操作~~~结果是因为要翻墙~~~