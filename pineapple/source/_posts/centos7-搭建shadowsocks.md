---
title: centos7 搭建shadowsocks
date: 2017-10-30 03:41:50
tags:
---
今天帮助小伙伴搭建了VPN(shadowsocks),在这里记录一下搭建的过程。
<!-- more -->
# 环境准备
1,国外的vps服务器。这里推荐[vultr](https://www.vultr.com/?ref=7144410)因为价格还算不错且速度快稳定，最主要的是可以直接destory sever（退款）！很良心啊有木有，对小白很贴心啊有木有！套餐选择最便宜的就好了。![](http://ww1.sinaimg.cn/large/006iB0xgly1fl0c53crbkj30xv0fawha.jpg)
2,centos7。我自己的服务器是centos6的，centos7也可以。
3,xshell。自己在网上可以搜到。
# 搭建过程
## 安装pip
首先用xshell连接远程服务器。账户名就是root，ip和password按照vps服务商提供的输入就可以。连接好之后是下面的样子：![](http://ww1.sinaimg.cn/large/006iB0xgly1fl0cg0qtyej30i10h8myc.jpg)
在shell里面输入以下命令：
``` bash
sudo yum -y install epel-release         #安装epel扩展源
sudo yum -y install python-pip           #安装python-pip
```
搞定！
## 安装shadowsocks

``` bash
pip install --upgrade pip                #升级pip
pip install shadowsocks                  #安装shadowsocks  
```
shdaowsocks已经安装完毕！至此环境已经搭建好了
## 编辑配置文件
这里写的是多用户的配置文件，如果想要单用户的自己随便搜一下官方文档就好了
首先：
``` bash
vi /etc/shadowsocks.json                 #创建配置文件 
```
然后在shell里输入insert进入编辑模式按如下配置：

``` bash
{"server":"yourip",                  
"port_password":{
     "8381":"password",
     "8382":"password",
     "8383":"password",
     "8384":"password",
     "8385":"password",
     "8386":"password"
     },
"timeout":600,
"method":"rc4-md5",
"fast_open":false,
"workers":1
}
```
之后esc，输入:wq保存文档
解释一下，"yourip"把yourip替换成你的真实ip地址，“password”里面替换成你的密码即可。
## 配置自启动
``` bash
vi /etc/systemd/system/shadowsocks.service                 #创建自启动文件 
```
按insert进入编辑模式：
``` bash
[Unit]
Description=Shadowsocks

[Service]
TimeoutStartSec=0
ExecStart=/usr/bin/ssserver -c /etc/shadowsocks.json

[Install]
WantedBy=multi-user.target
```
之后esc，输入:wq保存文档
执行以下命令启动 shadowsocks 服务：
``` bash
systemctl enable shadowsocks
systemctl start shadowsocks 
```
ok！服务已经搭建成功啦，最后关闭一下centos7的防火墙：
``` bash
systemctl stop firewalld.service                    #停止firewall
systemctl disable firewalld.service                 #禁止firewall开机启动
```
查看一下shdaowsocks的运行状态：
``` bash
systemctl status shadowsocks -l
```
如果运行成功应该是这样子的：
![](http://ww1.sinaimg.cn/large/006iB0xgly1fl0d0yjcmxj30he0alt9n.jpg)
# 客户端
客户端就很好办啦，点击[shadowsocks客户端下载](https://shadowsocks.org/en/download/clients.html)去下载对应的客户端就搞定了。
在这说一下，因为最近国内要求下架所有的vpn工具，所以现在苹果的appstore已经下载不到了。解决办法：去淘宝买一个美国的apple账号然后搜索“wingy”就好了。
最后按照你的服务端配置填写客户端就好啦！
# 结语
shadowsocks的安装就到这里了，下一篇博客还没想好写什么，因为实在水的很==。
