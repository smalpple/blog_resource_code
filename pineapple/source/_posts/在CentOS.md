---
title: 在CentOS 7下安装谷歌chrome
date: 2017-04-11 11:01:55
tags: 
categories: 杂项
---

### 配置下载yum源
<!-- more -->
在目录 /etc/yum.repos.d/ 下新建文件 google-chrome.repo

``` bash
[root@localhost ~]#    cd /ect/yum.repos.d/

[root@localhost yum.repos.d]#    vim google-chrome.repo
```
编辑google-chrome.repo，内容如下：
``` bash
[google-chrome]
name=google-chrome
baseurl=http://dl.google.com/linux/chrome/rpm/stable/$basearch
enabled=1
gpgcheck=1
gpgkey=https://dl-ssl.google.com/linux/linux_signing_key.pub
```
### 安装google chrome浏览器
``` bash
[root@localhost yum.repos.d]# yum -y install google-chrome-stable
```
PS: Google官方源可能在中国无法使用，导致安装失败或者在国内无法更新，可以添加以下参数来安装：
``` bash
[root@localhost yum.repos.d]# yum -y install google-chrome-stable --nogpgcheck
```