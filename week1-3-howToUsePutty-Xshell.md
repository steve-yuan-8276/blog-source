---
title: 'Linux运维学习笔记1-3：如何使用putty、xshell、iterm2进行ssh登陆'
date: 2018-03-14 12:12:01
categories: linux
tags: [centos, linux, putty, xshell, iterm2, notes] 
---

### 写在前面

这节课主要是学习如何使用shell工具进行远程连接，并设置秘钥认证。

### putty 和 xshell

#### 下载地址：

[putty官网](https://www.chiark.greenend.org.uk/~sgtatham/putty/) 最新版本是0.70

[xshell官网](https://www.netsarang.com/products/xsh_key_features.html) 最新版本是 xshell 5

#### 基本使用：

事实是，基本不使用。因为我用的是mac电脑。哈哈

看了教程，putty、xshell的连接过程基本上都是输入虚拟机ip地址、端口号、账户名、登陆密码之类的，大同小异。

教程在这里：

[putty和xsehll特点比较](https://www.netsarang.com/products/xsh_key_features.html)

[手把手教给你使用putty和xshell远程连接linux](http://blog.51cto.com/13518197/2050271)

<!--more-->

### iterm 2 

#### 下载安装

* 方法一： [官网](https://www.iterm2.com/index.html)  下载安装包，解压后拖到application文件夹即可。

* 方法二：brew安装

```
// 先安装 brew
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

// 安装brew cask
brew install caskroom/cask/brew-cask

// 安装iterm2
brew cask install iterm2
```

#### 基本设置

```
// 设置显示字体
iTerm2 -> Preferences -> Text -> Change Font -> Source Code Pro 15pt

// 设置窗口大小
iTerm2 -> Preferences -> Window -> Setting for New Windows -> Columns -> 100 -> Rows -> 30
```

iterm 2的更多使用技巧可以参见[这个教程](http://wulfric.me/2015/08/iterm2/)

### ssh连接虚拟机

```
// 终端输入
ssh username@xxx.xxx.xxx.xxx -p 22
```
![](https://lh3.googleusercontent.com/-051WtkX0xsE/WqjBsqnCRcI/AAAAAAABhio/soMdwI9cFFErcfmcBDxTBtPlq57Gg3z2QCHMYCw/I/15210090665231.jpg)

**注意事项**：

* 此处的username是cent os 中的账户名；

* xxx.xxx.xxx.xxx 是刚刚设置的静态ip；

* 22 表示连接的默认端口号，后期也可以进行编辑更改。

### 秘钥认证登陆

**总体思路：**

- 假设有两台电脑A和B，这里的A是你要操作的电脑；B是虚拟机。

- 先在A电脑生成密匙对（公钥、私钥各一个），私钥始终保存在A电脑不动，公钥复制出来，添加到电脑B的`authorized_ keys` 里面，再进行一些必要的设置，就可以从A电脑免密登陆B电脑了。

- 注意，如果已经在A电脑上设置过keygen，比如笔者已经在搞github折腾过一会，密匙对已经存在，就不用重新生成了，只要公钥复制出来粘贴过去就可以了。

####  生成密钥对 (本机操作)

##### 进入当前用户目录，一般root用户只需要这样即可

```
cd 
```
#####  创建.ssh目录并设置权限

```
mkdir -p .ssh
chmod 700 .ssh
```
##### 进入 .ssh 目录和生成密钥对

```
cd .ssh
ssh-keygen
```
然后，一路回车即可。

##### 注意事项：

* 一是 ssh-keygen 的详细用法，参见[ssh-keygen 中文手册]()(http://www.jinbuguo.com/openssh/ssh-keygen.html)

* 二是前面生成密钥的会显示地址，记住这个地址，需要把id_rsa.pub 的内容复制出来，后面会用到。

#### 生成密钥认证文件 （在服务器端或者通过ssh root操作）

##### 创建认证文件

```
touch authorized_keys
```

##### 编辑认证文件

```
vi /root/.ssh/authorized_keys
```

进入编辑界面后按i 开始编辑；把刚才复制的id_rsa.pub  内容复制到里面，稳妥起见，前面可以加一行注释，注释以#开头；

##### 保存并退出

按esc退出编辑状态，再按：wq 保存退出

##### 授权认证文件

```
chmod 600 authorized_keys
```

#### 修改SSH配置（在服务器端或者 ssh root操作）

##### 使用root登录修改配置文件：/etc/ssh/sshd_config

```
vi /etc/ssh/sshd_config
```
##### 将下面的内容的前面的 # 去掉

```
# PubkeyAuthentication yes
# AuthorizedKeysFile .ssh/authorized_keys

然后，修改下面的内容的 yes 为 no

PasswordAuthentication yes
```
修改后效果为

```
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
PasswordAuthentication no

```
##### 重启SSH服务

CentOS 6.x：

```
service sshd restart

```
CentOS 7.x：

```
systemctl restart sshd
```

#### 检验是否成功
 重启虚拟机，然后使用如下命令登陆
 

```
ssh root@xxx.xxx.xxx.xxx
```






