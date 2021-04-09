---
title: nodejs-project（Egg框架）
cover: /img/solar-system.jpg
# top_img: /img/universe1.jpg
date: 2020-12-15 15:18:12
tags:
---
使用nodejs在vue与java之间过渡一层，下面介绍使用nodejs搭建中间层后端项目
参考[eggjs官网](https://eggjs.org/zh-cn/intro/quickstart.html)
## Quick Start
### 全局安装Egg NodeJS前端框架脚手架
``` bash
$ npm i -g egg-init
```

### 创建项目
``` bash
$ egg-init {projectName} [--type=simple]
```
### 进入项目安装依赖
``` bash
$ npm i
```
### 本地启动项目
``` bash
$ npm run dev
```
### 安装NodeJS中间件、第三方模块和数据库
> 1. 安装mysql数据库使用
``` bash
$ npm i -s egg-mysql
# 若线上环境没用到mysql数据库，则不要配置下列项，启动加载时会找不到而报错
$ 在config/plugin.js里声明插件
exports.mysql = {
  enable: true,
  package: 'egg-mysql',
};
$ 在config/config.default.js里配置
config.mysql = {
  # 单数据库信息配置
  client: {
    host: 'localhost',
    port: '3306',
    user: '****',
    password: '*******',
    database: 'egg',
  },
  # 是否加载到 app 上，默认开启
  app: true,
  # 是否加载到 agent 上，默认关闭
  agent: false,
};
```

## 开发应用模式

### 请求响应模式
Router -> Controller -> Service -> MySQL
> 1. Router路由
``` javascript
router.get('/email', controller.email.getEmails);
```
controller.email的email是app/controller文件夹下的email.js文件，
email.js中的controller类必须导出才能使用（module.exports = EmailController;）  
controller.email.getEmails中的getEmails是email.js文件类中的一个方法  
当前端访问到该路由时，就是调用emailjs勒种的getEmails方法  
> 2. Controller控制器
``` javascript
async getEmails() {
  const ctx = this.ctx;
  const emails = await ctx.service.email.getEmails();
  ctx.body = emails;
};
```
在controller的getEmails方法中通过ctx调用service  
ctx.service.email的email是app/service文件夹下的email.js文件，
email.js中的service类必须导出才能被调用（module.exports = EmailService;）  
ctx.service.email.getEmails()中的getEmails是文件类中的一个方法  
当路由调用到controller类方法，在controller方法中会调用service类的方法  
> 3. Service服务
``` javascript
async getEmails() {
  let sql = 'select accountId from email';
  const emails = await this.app.mysql.query(sql);
  return emails;
};
```
在service的getEmails方法中通过this.app调用mysql  
await this.app.mysql.query(sql)异步调用mysql的查询sql语句，查询数据库  

获取数据return到controller，controller将其赋给ctx.body，前端会接收到返回数据  
> 4. MySQL数据库

通过/config/中的配置连接到环境中的数据库，运行sql语句，并将结果返回  

> controller负责与前端数据格式交互；service负责与数据库交互数据处理
### 自动调用（定时任务）模式
参考文档[eggjs定时任务](https://eggjs.org/zh-cn/basics/schedule.html)
1. app/schedule目录下建立定时任务文件send_email.js
2. 依赖Subscription，通过 schedule 属性来设置定时任务的执行间隔等配置（interval或者cron）；
subscribe 是真正定时任务执行时被运行的函数

