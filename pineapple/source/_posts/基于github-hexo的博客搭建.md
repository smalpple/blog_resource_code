---
title: 基于github+hexo的博客搭建(一)
date: 2017-03-15 12:36:37
tags:
categories: 杂项
---
因为本人意识兴起买了一个域名，本着不能浪费的原则，所以准备搭建一个博客(有点买了醋就差螃蟹的感觉==)。试了好多的方式，自己租了一个服务器，发现麻烦不说，服务器还经常出问题，所以上网查阅一下有关资料，发现基于githubpages+hexo这套博客系统不光方便，而且操作也特变简单。话不多说，直接上教程。
<!-- more -->
## 环境准备
### 安装nodes

到 [node.js](https://nodejs.org/en/)下载node.js最新版本一路安装。
``` bash
$ npm -v
```
如果出现版本号就证明你的node安装成功了。

### 安装gits
下载 [git](https://git-scm.com/)直接Next就可以了。

### 注册github，搭建仓库
#### 注册github
1，打开 [GitHub](https://github.com/)官网
2，填写注册信息进行注册操作。
#### 搭建仓库
1，登录github账号：在github首页点击Sign in按钮进入登录页面。填写用户名或邮箱和密码，点击Sign in按钮登录。
2，点击创建仓库：点击在登录的用户图像左边的+号和下三角符号按钮。
3，填写创建仓库信息：
![Alt text](https://raw.githubusercontent.com/smalpple/markdownimg/c732a08d5f3ef66bcf0c65bed63499d34b40db2a/2.PNG)
仓库名称必须是用户名.github.io，比如我的名称是smalpple，那么我的仓库名称就是smalpple.github.io
4，填写好相关信息，点击Create repository(创建仓库)按钮。
5，配置ssh
首先在桌面打开git bash终端：
``` bash
$ git config --global user.name "你的GitHub用户名"
$ git config --global user.email "你的GitHub注册邮箱"
```
生成ssh秘钥：
``` bash
$ ssh-keygen -t rsa -C "你的GitHub注册邮箱"
```
然后一直回车，此时，在用户文件夹下就会有一个新的文件夹.ssh，里面有刚刚创建的ssh密钥文件id_rsa和id_rsa.pub。
添加SSH公钥(把刚刚生成的id_rsa.pub文件用记事本打开)复制
到『Account settings -> SSH Keys -> Add SSH Key』
![Alt text](https://raw.githubusercontent.com/smalpple/markdownimg/master/3.PNG)
最后可以验证一下：
``` bash
$ ssh -T git@github.com
```
### 安装hexo
Node和Git都安装好后，就可以安装hexo啦：
``` bash
$ npm install -g hexo
```

到此为止，就已经把环境全部搭建完毕了!接下来就是搭建自己的博客啦。

## hexo搭建
### 初始化hexo
新建一个文件夹，命名blog(文件夹名字随意)
在此文件夹打开命令行：
``` bash
$ hexo init
```
### 安装依赖
``` bash
$ npm install
```
此时你的文件夹应该有这些文件
![Alt text](https://raw.githubusercontent.com/smalpple/markdownimg/master/4.PNG)
### 本地服务启动
``` bash
$ hexo s
```
此时在你的浏览器输入 http://localhost:4000，就应该能看到
你的hexo实例页面啦！

时间有限，本次关于hexo的讲解先到这，以后有空再继续更新关于hexo的教程。

### 附：最好的学习方式就是看文档[hexo](https://hexo.io/zh-cn/docs/)
