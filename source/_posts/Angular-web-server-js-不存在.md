---
title: Angular web-server.js 不存在
date: 2016-05-07 14:05:57
categories: Angular
tags: Angular
---


## 主要内容

在学习Angular，按照教程运行

> $ node scripts/web-server.js

遇到了如下错误

> Error: Cannot find module

也就是无法找到web-server.js文件，打开该文件夹发现还真没有这个文件。最后在网上找到了答案，是现在github的源文件放弃了这个启动方式，使用如下来启动命令

> $ npm start

最后就这样解决了这个问题

## 参考链接
- [http://www.tuicool.com/articles/ym6Jfen](http://www.tuicool.com/articles/ym6Jfen)
