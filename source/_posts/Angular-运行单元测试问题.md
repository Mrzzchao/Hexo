---
title: Angular 运行单元测试问题
date: 2016-05-07 22:02:17
categories: Angular
tags: Angular
---

## 问题
Angular真是一个很折腾人的框架，一天就遇到了两问题。

现在按照[Angular中文网](http://www.apjs.net/)的步骤进行单元测试时，又出现了问题。

首先我只想说这个网站的教程是多久以前的了，怎么源码文件和教程的命令不同步的，真是无力吐槽。

回到正题，由于本网站的年代性，原先

> .\scripts\test-server.bat

这些单元测试的命令是完全没用了，因为根本不存在test-server.bat文件

## 解决办法
再次感谢[JavaChen's Blog](http://www.tuicool.com/articles/ym6Jfen)写的教程
在他的博客里面执行

<!-- more -->
> npm run protractor

就可以运行单元测试了。。 但是，问题又产生了，执行该命令后会出现如下错误

    events.js:141
          throw er; // Unhandled 'error' event
          ^

    Error: spawn java ENOENT
        at exports._errnoException (util.js:870:11)
        at Process.ChildProcess._handle.onexit (internal/child_process.js:178:32)
        at onErrorNT (internal/child_process.js:344:16)
        at nextTickCallbackWith2Args (node.js:441:9)
        at process._tickCallback (node.js:355:17)

    npm ERR! Windows_NT 10.0.10586
    npm ERR! argv "F:\\Software\\nodejs\\node.exe" "F:\\Software\\nodejs\\node_modules\\npm\\bin\\npm-cli.js" "run" "protractor"
    npm ERR! node v4.2.6
    npm ERR! npm  v2.14.12
    npm ERR! code ELIFECYCLE
    npm ERR! angular-phonecat@0.0.0 protractor: `protractor test/protractor-conf.js`
    npm ERR! Exit status 1
    npm ERR!
    npm ERR! Failed at the angular-phonecat@0.0.0 protractor script 'protractor test/protractor-conf.js'.
    npm ERR! This is most likely a problem with the angular-phonecat package,
    npm ERR! not with npm itself.
    npm ERR! Tell the author that this fails on your system:
    npm ERR!     protractor test/protractor-conf.js
    npm ERR! You can get their info via:
    npm ERR!     npm owner ls angular-phonecat
    npm ERR! There is likely additional logging output above.

    npm ERR! Please include the following file with any support request:
    npm ERR!     E:\项目\public\angular-phonecat\npm-debug.log


这才是一个最磨人的bug，找了很多解决办法
- 更新谷歌浏览器
- 把protractor安装成全局的
    > npm install -g protractor

但是很遗憾以上两个办法对我都无效，在即将放弃之际，居然找到了解决办法，累死哥。

### 最终方法
把__angular-phonecat\test__下__protractor-conf.js__里的

> chromeOnly: true

换成

> directConnect: true

好了，再次启动，问题完美解决
