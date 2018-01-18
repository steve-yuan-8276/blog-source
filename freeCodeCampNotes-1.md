---
title: 'freeCodeCamp笔记：关于CSS优先级的一点常识'
date: 2017-12-22 09:00:49
categories: freeCodeCamp 
tags: [html, css, note] 
---

freeCodeCamp中文站: https://freecodecamp.cn

作为一个前端菜鸟，最缺的就是项目经验了。经人指点，说可以到freeCodeCamp来打怪升级。无奈这个网站是英文的，而我的英语又不在地。好在现在有了中文版的freeCode。

好吧，从此可以愉快滴刷题了！

刷题的过程，也是查漏补缺，复习知识点的过程，这里把一些以前忽视或者不明确的知识点整理记录下来。今天算是第一期，关于CSS优先级。

<!--more-->

### 前提准备
* 一个空白的html网页
* 一杯咖啡

### 优先级测试（从低到高）
##### Level 1 ：单独class样式
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>CSS 优先级测试</title>
    <style>
        .blue-text {
            color:blue;
        }
    </style>
</head>
<body>
    <h2 class="blue-text">测试文字</h2>
</body>
</html>
```

显示结果如下：
![](https://lh3.googleusercontent.com/-XAwmbZ5pvcM/Wjxd1JI_tbI/AAAAAAABfl0/drzsQtkOUpQPtXWN7eKd9Dv22VIKZxmDQCHMYCw/I/15139056181806.jpg)

这个没什么好说的。

#### Level 2 如果两个class样式相冲突，以后一个为准

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>CSS 优先级测试</title>
    <style>
        .blue-text {
            color:blue;
        }

        .red-text {           /*后写的red-text比先前的red-text级别高*/
            color:red;
        }
    </style>
</head>
<body>
    <h2 class="blue-text red-text">测试文字</h2>
</body>
</html>

```

显示结果如下：
![](https://lh3.googleusercontent.com/-ZW-3JYizirY/WjxfICME5MI/AAAAAAABfmA/QHqP0ciwkbga2YothK8cKThoVmLW5J_NwCHMYCw/I/15139059508364.jpg)

#### Level 3 ：加在id上的CSS优先级高于class

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>CSS 优先级测试</title>
    <style>
        .blue-text {
            color:blue;
        }

        .red-text {           /*后写的red-text比先前的red-text级别高*/
            color:red;
        }

        #yellow-text {        /*id写的CSS优先级高于class加的样式*/
            color:yellow;
        }
    </style>
</head>
<body>
    <h2 id="yellow-text" class="blue-text red-text">测试文字</h2>
</body>
</html>

```
显示结果：
![](https://lh3.googleusercontent.com/-SF-VXz5ziLU/WjxjA73mslI/AAAAAAABfmM/b8pXMYbiuQA-z5t9MrZSfXLvCFkT1Z5VACHMYCw/I/15139069463657.jpg)

看吧，是不是屎黄屎黄的？（太恶心了）

#### Level 4 ：行间样式优先级高于id上加的样式

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>CSS 优先级测试</title>
    <style>
        .blue-text {
            color:blue;
        }

        .red-text {           /*后写的red-text比先前的red-text级别高*/
            color:red;
        }

        #yellow-text {        /*id写的CSS优先级高于class加的样式*/
            color:yellow;
        }
    </style>
</head>
<body>
    <h2 style="color:pink" id="yellow-text" class="blue-text red-text">测试文字</h2>
    <!--行间样式的级别要高于id上加的样式-->
</body>
</html>

```
显示结果如下：
![](https://lh3.googleusercontent.com/-6mdjfBr-nU8/WjxkFN9cg-I/AAAAAAABfmY/eKSslbGy6pwT_tEzbLGrG06slvMAq90jQCHMYCw/I/15139072194318.jpg)

好吧，style越来越诡异了

#### level 5 ：传说中最高级别的大boss  '!important'

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>CSS 优先级测试</title>
    <style>
        .blue-text {
            color:blue !important;   /*!important 优先级最高*/
        }

        .red-text {           /*后写的red-text比先前的red-text级别高*/
            color:red;
        }

        #yellow-text {        /*id写的CSS优先级高于class加的样式*/
            color:yellow;
        }
    </style>
</head>
<body>
    <h2 style="color:pink" id="yellow-text" class="blue-text red-text">测试文字</h2>
    <!--行间样式的级别要高于id上加的样式-->
</body>
</html>

```

显示结果如下：

看吧，boss出手，传说中的blue又回来了。

**写在最后：**这些知识点虽然不难，但却是之前在学习中一直忽略的内容，正好借此机会补齐。

