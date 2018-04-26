---
title: Linux运维学习笔记：练习题目整理
date: 2018-04-24 18:28:15
categories: linux
tags: [centos, linux, shell, notes] 
---

### 写在前面

这则笔记整理了一下shell基础知识的课后练习题及其解答。

### 作业题：

#### 1. 设置环境变量 HISTSIZE , 使其能够保存10000条命令历史。

**解答**

方法一：export命令

```
export HISTSIZE=10000
```

方法二：vim编辑`/etc/profile`,将HISTSIZE的值改为10000，之后保存退出，`source /etc/profile`


#### 2. 为什么如果这样设置PS1 `PS1="[\u@\h \W]\$ "`  显示的结果和我们预想的不一样，那要如何设置才能恢复原来默认的？

**解答：**

如图所示，设置变量应该使用单引号；如果使用双引号，要再加上脱义符`\`

![](https://farm1.staticflickr.com/831/27821979868_13f909edcd_o.png)

具体的设置方法参见第一题的解答。

<!--more-->

#### 3. 想办法把当前目录下的文件的文件名中的小写字母全部替换为大写字母。

解答：

使用tr命令替换字符，ls | tr '[a-z]' '[A-Z]' ，如下图所示：

![](https://farm1.staticflickr.com/974/40792275815_51d87486c2_o.png)

#### 4. 使用sort以":"为分隔符，对/etc/passwd文件的第5段排序。

**解答：**

主要考察sort用法，-t选项指定分割符，-k选项指定域；

```
cat /etc/passwd | sort -t ':' -k 5
```
如下图所示：

![](https://farm1.staticflickr.com/869/40792341185_666cd3dc53_o.png)


#### 5. 使用cut以":"为分隔符，截出/etc/passwd的第三段字符。

**解答：**

主要考察cut用法，`-d` 选项指定分割符；`-f`选项指定域。

```
cat /etc/passwd | cut -d ':' -f 3
```

如下图所示：

![](https://farm1.staticflickr.com/824/27822366118_0800e8c37c_o.png)


#### 6. 简述这几个文件的作用： /etc/profile, /etc/bashrc, .bashrc, .bash_profile.

**解答：**

配置文件|作用
---|----
`/etc/profile`|配置所有用户共同的环境变量，当用户登录时总是会首先读取这个文件
`/etc/bashrc`|每一个运行bash shell的用户都执行此文件，此外还有PS1,umask的设置
`.bashrc`|每个用户的bash设置，用户登录shell或者新打开shell时都会读取此文件，以no-login的方式交互
`.bash_profile`|用户自己的环境变量，可以在其中设置一些自己使用shell信息，是以login的交互方式进行的


#### 7. export 的作用是什么？

**解答：** `export`命令用于显示和设置环境变量，命令行格式：`export A='Alibaba'`  其中，A代表变量名，`'Alibaba'`代表变量内容。

#### 8. linux下自定义变量要符合什么样的规则呢？  

**解答：**

命令行格式：`export A='Alibaba'`  其中，A代表变量名，`'Alibaba'`代表变量内容。设置变量要符合以下规则：

* `= `等号两边不能有空格；

* 变量名只能由英、数字以及下划线组成，而且不能以数字开头；

* 当变量内容带有特殊字符（如空格）时，需要加上单引号；

* 如果变量内容中需要用到其他命令运行结果则可以使用反引号；

* 变量内容可以累加其他变量的内容，需要加双引号；


#### 9. 如何把要运行的命令丢到后台跑？又如何把后台跑的进程给调到前台？

**解答：** 在命令行后面加`&`，表示background的意思；查看后台运行程序可以使用`jobs`命令；如果要调回前台，使用`fg`。

![](https://farm1.staticflickr.com/863/27822628878_54b6dae1f8_o.png)


#### 10.  列出当前目录下以"test"开头的文件和目录。

解答：

- 主要考察`grep`的用法，`^`表示起始位置；` $`表示结束位置;

`ls | grep '^test'` 查找当前目录下文件名以test打头的文件

![](https://farm1.staticflickr.com/959/27822684478_d1b530b2b9_o.png)

- 更简单的解决办法，*可以表示任意字符

`ls test*` 联同子目录的都一起匹配出来了。

![](https://farm1.staticflickr.com/829/39884910260_e39774827f_o.png)

#### 11.  如何把一个命令的输出内容不仅打印到屏幕上而且还可以重定向到一个文件内？

**解答：**

该题目主要涉及管道符和tee命令知识，`cat /etc/passwd | tee b.txt` 如下图所示:

![](https://farm1.staticflickr.com/871/41692003741_cc6364e5cb_o.png)

#### 12. 假如有个命令很长，我们如何使用一个简单的字符串代替这个复杂的命令呢？请举例说明。

**解答：**

这道题是在考查设置alias的知识。

- 第一种方法：alias 命令

```
alias short=long
```

- 第二种方法：使用`vim` 更改配置文件，只想更改当前用户的话就在 `~/.bashrc` 设置；更改全局配置的话，就在 `/etc/bashrc` ，设置完成保存退出，执行 如下命令生效：

```
source ~/.bashrc
```


#### 13. 我如何实现这样的功能，把一条命令丢到后台运行，而且把其正确输出和错误输出同时重定向到一个文件内？

**解答：**

这道题考查输出重定向，以及后台运行的命令` &`

最方便的用法 `&>` 

![](https://farm1.staticflickr.com/951/40977485114_a049bf872d_o.png)

#### 14. 如何按照大小（假如按照10M)分隔一个大文件，又如何按照行数(假如10000行)分隔？

**解答：**

此题考查split 命令,命令行格式：`split [参数] [需要切割的文件] [指定切割文件名的前缀]` ，其中`-b` 表示按大小切割；`-l`表示按行数切割；

假定需要切割的文件名为a.txt，指定切割为前缀为yf-

```
split -b 10M a.txt yf- 
```

假定按照10000行一组进行切割

```
split -l 10000 a.txt yf-
```

#### 15. 做实验，搞明白 ; && || 这三个符号的含义。

**解答：**

* `; `多条命令在一条命令中是执行，各条命令间并无关联；

* `&& `相当于是"且"的关系,只有前一条命令执行成功后一条命令才执行；

* `||` 相当于“或”，前一条命令执行成功，后一条命令不执行；前一条命令不执行，后一条命令才执行；两条命令，总有一条执行。


#### 16. 如果只想让某个用户使用某个变量如何做？

**解答：**

这道题目的意思应该是，如何设置当前用户的变量，而不是全局变量，实质是在问` /etc/profile` 和 `～/.bash_profile` 的区别：

* `/etc` 是存储存储系统变量的文件目录，自然`/etc/profile`定义的就是全局变量，会影响到所有用户；

* `～` 是当前用户的家目录，在这里的配置文件只会影响当前用户；

综上所述，如果只想定义当前用户的变量环境，在`～/.bash_profile`配置即可。


#### 17. 使用哪个命令会把系统当中所有的变量以及当前用户定义的自定义变量列出来？

**解答：**

`set` 命令：显示系统所有的变量和当前用户自定义的变量

类似的命令还有env ：显示用户变量。

更多的笔记，在[Linux运维学习笔记5-4：shell基础知识（二）](https://www.steve-yuan.com/2018/04/17/week5-4-basisOfShellPart2/)


### 扩展阅读：

* [Linux环境变量之“PS1"](http://www.lishiming.net/thread-5364-1-1.html) 

* [Linux支持中文](http://www.lishiming.net/thread-5360-1-1.html) 

* [让命令历史永久保存并加时间戳](http://www.lishiming.net/thread-283-1-1.html) 

* [linux 下/etc/profile、/etc/bashrc、~/.bash_profile、~/.bashrc 是干啥的](http://www.lishiming.net/thread-909-1-1.html) 

