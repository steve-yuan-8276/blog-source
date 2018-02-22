# JS学习笔记：JavaScript常用基础知识整理

### 类型和类型转换

JavaScript中有7个内置类型：null，undefined，boolean，number，string，object，和symbol(ES6)；除了object以外，其它都叫做基本类型。

#### Null vs. Undefined

* **Undefined**表示未定义。对于没有初始化的变量、函数调用时候未提供的函数参数、缺失的对象属性，它们的默认值就是undefined。如果一个函数没有返回语句，那么默认的返回值也是undefined。

* **NUll**表示值为空。一个变量我们可以将其赋值为null，表示当前的没有值。

#### 隐式转换

```
var name = 'Joey';
if (name) {
  console.log(name + " doesn't share food!")  // Joey doesn’t share food!
}
```
这里采用了隐式转化，就是当name == true ，则执行下面的语句；反之，当name == false，则不执行。

""，0， null，undefined, NaN, false 会自动转换为false。其它的都会转换为真。

#### == vs. ===

* ==在验证相等性的时候，会对类型不同的值做一个类型转换。
* ===对要判断的值不做类型转换。

```
2 == '2'            // True
2 === '2'           // False
undefined == null   // True
undefined === null  // False
```

一些比较容易出错的例子：

```
false == ""  // true
false == []  // true
false == {}  // false
"" == 0      // true
"" == []     // true
"" == {}     // false
0 == []      // true
0 == {}      // false
0 == null    // false
```

https://blog.fundebug.com/2018/01/15/the-definitive-javascript-handbook-for-a-developer-interview/

https://juejin.im/post/5a80fff0f265da4e7b44a7fc

https://juejin.im/post/5a810556f265da4e9f6fa465

