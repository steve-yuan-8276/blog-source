---
title: 'HEXO折腾笔记：给自己的博客做个美容'
date: 2018-01-23 22:44:27
categories: hexo 
tags: [hexo, github, next] 
---

### 写在前面

其实早就想折腾，一来忙着换工作，没心情；二来水平很菜，怕一不小心搞坏了。不过就想很多事情一样，心急吃不热豆腐。有些事情还是急不来的，所以……让我coding一下，冷静冷静。

是的，学习，让我们感觉到很踏实。

### fork me on github

#### 实现效果
![](http://oslz30y7b.bkt.clouddn.com/18-1-23/32483058.jpg)

#### 实现方法

1）通过github-ribbons或github-corners，寻找合适的图标，把代码复制下来；
![](http://oslz30y7b.bkt.clouddn.com/18-1-23/25770231.jpg)

2）打开` themes/next/layout/_layout.swig `文件，把代码复制到`<div class="headband"></div>`下面。

<!--more-->

### 静态网页压缩

#### 1）在站点的根目录下执行以下命令：

```
$ npm install gulp -g
$ npm install gulp-minify-css gulp-uglify gulp-htmlmin gulp-htmlclean gulp --save
$ touch gulpfile.js  //新建 gulpfile.js
```
#### 2）采用atom 打开gulpfile.js，复制粘贴以下代码：

```
var gulp = require('gulp');
var minifycss = require('gulp-minify-css');
var uglify = require('gulp-uglify');
var htmlmin = require('gulp-htmlmin');
var htmlclean = require('gulp-htmlclean');
// 压缩 public 目录 css
gulp.task('minify-css', function() {
    return gulp.src('./public/**/*.css')
        .pipe(minifycss())
        .pipe(gulp.dest('./public'));
});
// 压缩 public 目录 html
gulp.task('minify-html', function() {
  return gulp.src('./public/**/*.html')
    .pipe(htmlclean())
    .pipe(htmlmin({
         removeComments: true,
         minifyJS: true,
         minifyCSS: true,
         minifyURLs: true,
    }))
    .pipe(gulp.dest('./public'))
});
// 压缩 public/js 目录 js
gulp.task('minify-js', function() {
    return gulp.src('./public/**/*.js')
        .pipe(uglify())
        .pipe(gulp.dest('./public'));
});
// 执行 gulp 命令时执行的任务
gulp.task('default', [
    'minify-html','minify-css','minify-js'
]);
```
3）更新推送

```
hexo g
gulp
hexo d

```

https://www.jianshu.com/p/efbeddc5eb19?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation

https://www.jianshu.com/p/f054333ac9e6?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation

