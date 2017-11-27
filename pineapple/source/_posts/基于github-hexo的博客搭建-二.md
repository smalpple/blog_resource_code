---
title: 基于github+hexo的博客搭建(二)
date: 2017-03-16 17:58:13
tags:
categories: 杂项
---
上篇讲到了如何在本地启动hexo服务，再补充几个常用命令：
``` bash
$ hexo s --debug  #开启调试模式，可以对hexo框架修改后及时预览自己的博客
$ hexo n   #写文章
$ hexo g   #生成
$ hexo d   #部署 # 可与hexo g合并为 hexo d -g
```
这篇会讲到如何将你的博客托管在github上，并且和你自己的域名关联（前提是你要有一个域名）
<!-- more -->

## 将你的博客托管在github上
### 设置github
打开你之前创建的git仓库:
![Alt text](https://raw.githubusercontent.com/smalpple/markdownimg/master/6.PNG)
点击界面右侧的Settings，你将会打开这个库的setting页面，向下拖动，直到看见GitHub Pages
点击Automatic page generator，Github将会自动替你创建出一个gh-pages的页面。
如果你的配置没有问题，那么大约15分钟之后，yourname.github.io这个网址就可以正常访问了~
如果yourname.github.io已经可以正常访问了，那么Github一侧的配置已经全部结束了。
### 关联本地框架与git
打开你本地hexo的文件夹，在根目录下找到_config.yml,找到deploy:选项，修改成：
![](http://ww1.sinaimg.cn/large/006iB0xgly1fdy2ovqiimj30gl04c74a.jpg)
其中repo：选项改成你的仓库地址，然后：
``` bash
hexo d -g     #生成并部署你的博客到github上
```
不出意外的话，稍等一会后（15分钟之内）在浏览器输入你的仓库地址，我的是（http://smalpple.github.io/），就可以看到你的博客啦！到此，博客的框架已经搭建成功
## 关联你的域名
这个步骤的前提是你要有你自己的域名，如果没有可以自己买一个(推荐阿里云or腾讯云)或者跳过此步骤==
我们需要配置一下域名解析。推荐使用DNSPod的服务，比较稳定，解析速度比较快。在域名注册商出修改NS服务器地址为：
``` bash
f1g1ns1.dnspod.net
f1g1ns2.dnspod.net
```
以dnspod为例，点击域名管理进入管理页面 => 点击域名后面的管理 => 进入域名管理的操作界面，点击域名管理，来到域名管理界面 => 点击修改域名DNS，然后选择填写具体信息，在下面的空框中填入DNSPod的NS服务器
接着，我们进入DNSPod的界面，开始真正进入域名解析的配置。在DNSPod中，首先添加域名，然后分别添加如下条目：
![](http://ww1.sinaimg.cn/large/006iB0xgly1fdy2ii4nlqj30m605r74g.jpg)
自己本地的hexo目录下的source文件夹中，新建一个CNAME文件，里面写入你要绑定的域名，比如[koreyoshi.win](http://koreyoshi.win/)。
然后执行：
``` bash
$ hexo d -g 生成并把你的代码部署到github上

```
这一系列的操作中，包括修改NS服务器，设置A解析等等，都需要一定的时间。短则10分钟，长则24小时，最长不会超过72小时。如果超过72小时，请检查自己的配置过程，或者修改自己本地的DNS服务器。然后输入你的域名就可以看到你的博客啦！

## 预告
本篇博客到此为止，下一篇我将更新如何写自己的文章，如何修改主题以及如何添加评论，当然还有最最重要的，如何将你的博客提交给搜索引擎！（虽然对我来说现在并没有什么卵用，因为阅读量还没有到两位数==）
