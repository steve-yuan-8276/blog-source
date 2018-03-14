---
title: 'Linux运维学习笔记1-1：初识centOS7'
date: 2018-03-14 10:22:02
categories: linux
tags: [centos,linux, notes] 
---

### 写在前面

之前断断续续自学过一部分，现在拿到了猿课的学习计划，索性按照这个计划重新系统整理一遍。

### Linux基础知识

Linux跟MacOS、Windows一样，都是计算机操作系统，不同之处在有两点：

* 一是开源（大部分是免费的）；

* 二是多用在服务器领域（学习这个就是为了转行找工作，不是嘛）

<!--more-->

### 常见的Linux发行版

系统名称| 官网 | 特点 | 备注
---|---|---|---
Ubuntu| https://www.ubuntu.com/|目前最流行的个人版Linux系统，界面做得比较美观。| 使用apt安装和更新软件
Red Hat Enterprise（RHEL）| https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux | 面向企业的server版本，也是应用最广泛的server版本。| 需要授权付费才能使用yum工具
centOS| https://www.centos.org/|CentOS与RHEL 100%兼容，更重要的是完全免费。| 使用yum工具安装和更新软件
Debian| https://www.debian.org/| 元老级的linux版本，也非常适合英语server| 使用apt或aptitude来安装和更新软件

### 安装虚拟机

#### 虚拟机选择：

虚拟机| 官网 | 特点 |备注
---|---|---|---
 VirtualBox| https://www.virtualbox.org/wiki/Downloads |免费，适用于mac、Windows 
VMware fusion | https://store.vmware.com/store?Action=home&Locale=en_US&SiteID=vmware| 付费，使用与mac和wondows |价格居中，尤其是在某宝上
parallel desktop | https://www.parallels.com/cn/products/desktop/ |付费，适用于mac和windows |价格最贵，不过近两年都有bundle

安装都是傻瓜式，一路默认下一步即可。

### 安装centOS7

#### 下载地址：
 
* 官方镜像：[CentOS官网](https://www.centos.org/download/) 

* 国内镜像：[搜狐](http://mirrors.sohu.com/centos/)、[163](http://mirrors.163.com/centos/)、[阿里巴巴](https://mirrors.aliyun.com/centos/)

#### 新建虚拟机：

##### 安装注意要点：

1. 在“自定义硬件”的选项中，网络适配器建议选择NAT模式，兼容性最好。

2. 在系统“安装位置”中，选择“我要配置分区”，自定义系统分区；在 LVM下拉菜单，选择 “标准分区”，之后点击加号手动进行修改，点击“添加挂载点”，最后点击“完成”，保存“接收更改”。

3. 虚拟机分区原则：

分区名称| 空间大小
---|---
/boot| 200M
/swap | 4G
/ | 20G
/data | 剩余磁盘空间

**注意：**

1. 如果是虚拟机仅仅用来学习linux，磁盘空间有限的情况下，处 `/boot` 、`/swap` 之外的空间都可以分给 / 根目录，没有必要再分出` /data` 了。

2. swap分区大小跟物理内存大小有关，通常建议如下：

物理内存 | SWAP分区
---|---
4G以内| 内存的2倍
4-8G | 等于内存大小
8-64G | 8G
64-256G| 16G




