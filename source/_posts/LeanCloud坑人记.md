---
title: LeanCloud坑人记
date: 2016-04-18 14:15:24
categories: Hexo
tags: LeanCloud
---


![LeanCloud](http://7xrul1.com1.z0.glb.clouddn.com/leancloud.png)

<!--more-->

# 前言
按照[Next官方手册](http://theme-next.iissnan.com/getting-started.html)给的[LeanCloud教程](https://notes.wanghao.work/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%85%8D%E7%BD%AELeanCloud)
弄完以后，次数格式出现了xx:xx:xx的形式，当时的内心是崩溃的。Why?经多方的研究和询问以后发现是因为**Next主题**已经集成了LeanCloud，而我们只需要配置`主题_config.yml`即可，但是，坑爹的又出现了，把教程里面的配置过的东西删除后，次数就完全不显示了，再次经过多方的研究，解决了这个问题，所以在此记录

# 配置LeanCloud
见[LeanCloud教程](https://notes.wanghao.work/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html#%E9%85%8D%E7%BD%AELeanCloud) **配置LeanCloudLean**部分，请无视前面内容

> **注意**：后面的 **Web安全** 模块要配置，要不会不行，至少本人配置后才能正常使用



# 关键部分
如果你已经按照教程配置第三方LeanCloud后不行的，那就看这里了。我的解决办法就是重新克隆Clone **Next** 主题

> 温馨提示： 在克隆前记得先备份原来的主题文件，以免配置丢失。另外提醒，如果重新登录以后不能正常显示，完全可能是浏览器缓存问题。最后推荐大家可以把hexo的整个文件**Git**到**Github**上，详细过程不一一讲述了
