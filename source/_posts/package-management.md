---
title: npm和yarn常见命令
cover: /img/star4.jpg
date: 2020-12-10 09:33:29
tags:
---
npm and yarn package management common command

# npm和yarn命令
## 查看版本
``` bash
$ npm -v
$ yarn -v
```
## yarn安装
``` bash
$ npm i yarn -g
```

## npm\yarn
| npm | yarn | 说明 |
| :---:| :---: | :---: |
| npm init | yarn init | 初始化某个项目 |
| npm install/link | yarn/ yarn install | 默认的安装项目所有依赖 |
| npm install -S pkg@version | yarn add pkg@version | 安装某个依赖包（dependencies） |
| npm uninstall -S pkg@version | yarn remove pkg@version | 移除某个依赖包 |
| npm install -D pkg@version | yarn add pkg@version -D | 安装某个开发时（devDependencies）的依赖包 |
| npm update -S pkg@version | yarn update pkg@version | 更新某个依赖包 |
| npm install --global/-g pkg@version | yarn global add pkg@version | 安装某个全局依赖包（整个环境） |
| npm run/test xxx | yarn xxx  | 运行某个命令 |
| npm run serve | yarn serve | 本地编译运行命令 |
| npm info pkg | yarn info pkg | 显示某个pkg包信息 |
| npm list | yarn list | 列出项目的所有依赖 |
| npm config | yarn config | 管理 yarn 配置文件 |
| npm config list | yarn config list | 显示当前配置 |
### 注意
在package.json中的两个字段：
dependencies：是在生产环境中运行需要的安装包
devDependencies：是在开发环境中需要安装的依赖包





