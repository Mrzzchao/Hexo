---
title: Yeoman 浅析
date: 2016-08-26 01:32:40
categories: Yeoman
tags: gulp-angular
---


## 前言
当项目达到一定规模时，相信每个人都在烦恼，目录结构、各种包、依赖的安装，这些是很影响效率的。所以呢，一个神奇的脚本架---Yeoman出现了。那什么是脚本架呢，官网解释是这样的
> Yeoman helps you to kickstart new projects, prescribing best practices and tools to help you stay productive

简单来说，就是一切帮你自动达好框架，你只要按着他的生成器教程来编写代码就可以了，[Yeoman官网][1]


 
## 安装Yeoman
### 准备
在安装Yeoman之前应该先搭好环境，应该是什么环境呢，当然是**Node**了，这个就不多解释了，[Node安装][2]


### 安装 Yo
很简单，把他安装到全局里，命令如下

<!-- more -->
```shell
npm install -g yo
```

### 安装生成器（Generators）
安装好yo 之后呢，我们需要在安装我们需要的生成器，什么是生成器呢？其实就是项目模板，而Yo只是创建这模板的指挥员而已

所以，我们需要选择我们复合需求的生成器，官网里已经有很多已经搭建好的生成器，[详情][3]

而命令也很简单，以我后面会详细讲的**gulp-Angular**为例

在这之前，先安装依赖的**gulp**和**bower**

```shell
npm install -g yo gulp bower
```

然后，安装生成器
```shell
npm install -g generator-gulp-angular
```

### 运行生成器
安装完成后，我们先创建一个我们的项目目录，并进入目录

```shell
mkdir my-new-project && cd $_
```

然后运行我们的生成器

```shell
yo gulp-angular
```

之后只要按提示选择我们需要安装的包就可以了


## Gulp-Angular生成器简单解析

> 配置选择：angular,ui-router,bootstrap,jq,es6,resource

### 生成目录
当以上都执行完以后，应该会呈现如下目录
![此处输入图片的描述][4]

如果没有**bower_componets**或者**node_modules**目录，那就需要手动安装了,执行

```shell
npm install   // 生成node_modules
bower install // 生成bower_componets
```
- **bower_componets:** bower.json中的依赖包目录

- **e2e:** 测试目录

- **gulp:** gulp配置目录

- **node_modules:** package.json里面依赖包目录

- **src:** 源文件目录（也就是我们主要编码，处理过的）

- **.bowerrc:** bower配置文件，可以设置安装位置

- **.gitignore:** 配置Git上传时忽略文件名

- **bower.json:** bower 安装的依赖配置

- **gulpfile.js:** gulp 运行的入口文件，和**makefile**同理

- **karma.conf.js:** karma 测试文件

- **package.json:** npm 安装的配置

- **protractor.conf.js:** Angular 专门的测试框架

接着，在项目根目录执行

```shell
gulp
```

会多出**.tmp**和**dist**目录

- **.tmp:** 处理过程的临时文件

- **dist:** 进行各种注射，压缩等处理后的项目文件
![此处输入图片的描述][5]
 

### Gulp 运行
其实脚本架之所以能高效率的帮助我们完成项目的构建，这完全归功于这神奇的**[Gulp][6]**，用自动化构建工具增强你的工作流程

当运行`Gulp`时，其实里面发生了很多事情，现在我就开始简单归纳一下流程


![此处输入图片的描述][7]

![此处输入图片的描述][8]

![此处输入图片的描述][9]

 1. 通过**src/app** 下的**index.module.js**和**index.scss**文件作为**src**下其他**js**和**scss**文件的接入口，全部导入到这两个文件中

 2. 将**index.module.js**进行各种处理后，输出到**./tmp/serve/app**目录下的**index.module.js**文件

 3. 将**index.scss**各种**scss**文件的注入后，输出到**./tmp/serve/app**目录下的**index.scss**文件

 4. 把**.tmp/serve/app**和**bower_componets**下的**css**与**js**文件通过**link**与**script**注射到**src**目录下的**index.html**文件里，然后输出到**.tmp/serve**下的**index.html**文件

 5. 将**.tmp/serve**下的**index.html**所有**script**标签的**js**文件合并压缩输出到**dist/scripts**目录下。其中,**app.*.js**为用户自己编写代码的输出文件，**vendor.*.js**为所有**js**依赖的输出文件

 6. 将**.tmp/serve**下的**index.html**所有**link**标签的**css**文件合并压缩输出到**dist/styles**目录下。其中,**app.*.css**为用户自己编写代码的输出文件，**vendor.*.css**为所有**css**依赖的输出文件

 7. **bower_componets**目录中的字体文件输出到**dist/fonts**目录中

 8. 最后将其他文件原样输出到**dist**目录中，并对**src**目录下所有**html**与**scss**文件以及项目根目录下的**bower.json**文件进行监视

### Gulp 文件

 ![此处输入图片的描述][10]
 
- **conf.js:** 提供一些全局变量 

- **build.js:**  作为第一个最主要的任务，将其他任务结合构建起来，关键模块如下

    - **useref:** 通过`<!-- build:js(src) scripts/vendor.js --><!-- endbuild -->`等标志，将在其中的标签标示的文件输出成一个文件和一个标签

- **inject.js:**  负责将js和css文件注射进html文件，关键模块如下

  - **inject:** 通过`<!-- inject:js --><!-- endinject -->`等标志将指定的源文件文件注入
  
  - **wiredep:** 通过`<!-- bower:js --><!-- endbower -->`等标志将bower.json依赖的文件注入

- **styles.js:** 将**src**下和**bower**的**scss**文件注入到**index.scss**中，并编译后输出到**./tmp/serve/app**目录下的**index.scss**文件

- **scripts.js:** 将**index.module.js**进行各种处理后，输出到**./tmp/serve/app**目录下的**index.module.js**文件

- **server.js:** 处理一些`gulp command` 和服务的开启

- **watch.js:** 对文件进行监视

- **其他两个:** 测试


## 参考
### [Gulp文件注释][11]


  [1]: http://yeoman.io/
  [2]: http://nodejs.cn/
  [3]: http://yeoman.io/generators/
  [4]: http://7xrul1.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20160825225634.png
  [5]: http://7xrul1.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20160825232421.png
  [6]: http://www.gulpjs.com.cn/
  [7]: http://7xrul1.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20160825234115.png
  [8]: http://7xrul1.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20160825234058.png
  [9]: http://7xrul1.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20160825234127.png
  [10]: http://7xrul1.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20160825233345.png
  [11]: https://github.com/Mrzzchao/Demo/tree/master/Ng/Ang/gulp