---
title: 'Linux运维学习笔记1-2：如何配置静态IP'
date: 2018-03-14 11:57:08
categories: linux
tags: [centos, linux, ip, notes] 
---

### 主要内容

这节课主要是如何设置静态ip及过程中的网络问题排查。

### 设置网络静态IP

#### 获取IP地址信息

在登录框中输入以下命令，获取ip地址

```
dhchlient    // 自动获取ip地址
```

可以通过ping命令来验证网络是否联通

```
ping -c 4 www.163.com
```

查看当前网络状况，使用命令

```
ip addr    // 查看ip地址信息
```

`需要注意的是，这里需要记下来ip address、gateway、netmask、ensXX（网卡信息），后面设置静态ip会用到。

<!--more-->

#### 编辑网卡配置

```
# vi /etc/sysconfig/network-scripts/ifcfg-ens33
```
注：此处的XX，就是前面查到的网卡信息。

```
ONBOOT=yes；//表示网卡随系统一起启动
BOOTPROTO=static // 用来设置网卡启动类型，dhcp表示自动获取ip地址，static表示手动设置ip地址
IPADDR=xxx.xxx.xxx.xxx  //dhclient获取的网址
NETMASK=255.255.255.0    //子网掩码
GATEWAEY=xxx.xxx.xxx.xxx     //网关地址
DNS1=119.29.29.29    //DNS服务器地址，这里提供的一个公共DNS
```

最后，先按“esc”退出编辑模式，之后再输入“:wq”进行保存。


#### 重启ip设置

```
systemctl restart network.service

```
正常情况下，静态ip就设置好。检查是否成功，可以ping一下外网，如：

```
ping -c 4 www.163.com
```

#### Troubleshooting

按照教程进行到这一部后发现网络不通，提示错误 `name or service not know` ，又是一番折腾。这样要注意的是：

* ip和网关必须是在同一个网段；

* DNS设置错误也会出错，如果这个DNS地址不行，就试试8.8.8.8



