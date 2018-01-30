REACT学习笔记：REACT基础

### 编程环境搭建

* Homebrew
* Git
* Sublime as Editor
* iTerm2 (Optional)
* GitHub

#### Homebrew 包管理

##### Installation
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

##### uodate homebrew：
```
brew update in
```

#### Git  版本管理

##### Installation：

```
brew install git
```

##### 

```
git --version
```

#### Sublime 编辑器

##### Installation ：

```
brew install caskroom/cask/brew-cask
brew tap caskroom/versions
brew cask install sublime-text
```
##### Verify if the installation was successful:

```
sublime --version
```
##### open any directory from the command line with `sublime + <fileName>`
```
link: ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/sublime
```

#### iTerm2 终端替代品

##### Installation：

```
brew cask install iterm2
```

#### Node 和 Npm

DownLoad：[https://nodejs.org](https://nodejs.org/en/)

Documentation 在[这里](https://nodejs.org/en/docs/)

##### Verify if the installation was successful:

```
node --version
npm --version
```

##### howToUse:

```
npm install -g <package>    //全局安装，可以在任意文件夹使用
npm install <package>     //本地安装，只能在安装文件夹里使用
```

##### 初始化

```
npm init -y
```
-y 标记将把你的 package.json 内容初始化成默认值。如果你不加这个标记，就需要特别设 置该文件的内容。完成 npm 项目初始化之后，你就可以通过 npm install < 包名 > 来安装 新的 node 包了。

#### 安装 React

##### 方法一：通过 CDN (content delivery network)

在HTML文件head部分插入：

```
<script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>

<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
```
WARNING：官方DOCS有一句警告：`only meant for development, and are not suitable for production. ` 很机智的赶脚！

##### 方法二：npm安装

```
npm init -y    //前提：初始化npm 项目和 package.json 文件
npm install react react-dom
```

### 零基础创建react应用 create-react-app

#### Instalation：

```
npm install -g create-react-app
```
#### Verify if the installation was successful:

```
create-react-app --version
```
#### 创建react应用

```
create-react-app hackernews
cd hackernews
```

安装完之后的文件目录结构如下：
![](https://lh3.googleusercontent.com/-myuygpcX7Rg/WnAWZ06fVgI/AAAAAAABgKc/qRt3LXGiB9MLWXtUHZOCDidZxAfKYIK6ACHMYCw/I/15172952052835.jpg)

其中需要关注的文件夹有：

* README.md 说明文档

* src/ ：重点关注，所有需要的文件都可以在这里找到。

* public/: 包含了所有你的项目构建出的产品文件。最终所有你写在 src/ 文 件夹里面的代码都会在项目构建的时候被打包放在 public 文件夹下。

其他有用的npm命令

```
npm start   // 在 http://localhost:3000 启动应用 

npm test     // 运行所有测试 

npm run build     // 构建项目的产品文件 
```




