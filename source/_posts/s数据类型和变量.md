title: js数据类型和变量
author: 郭峰
tags:
  - 前端基础
categories:
  - js
date: 2019-12-28 12:28:00
---
# js数据类型
* undefined
* null
* string
* boolean 
* number
* symbol(ES6)
* Object

## 基本数据类型
##### 1：数字（number）
* 包括了浮点数和整数；
> 大多数语言在计算浮点数时都会出现计算不精确的问题，这是由于计算机在计算的时候会将数组转换成二进制数，因为二进制表示太长了，计算机会截取一定的位数来进行计算，所以在计算浮点数时会出现一些不精确的问题，但是，这种现象在js中尤为严重解决方式一般是先将浮点数转换成整数（乘以固定的十的倍数，之后再结果上除去），在网上有很多封装好的函数来进行这个动作

<!--more-->
* 八进制：以数字0开始表明该数字的八进制；
* 十六进制：以0x或者0X为前缀，表示数字为十六进制；
* 特殊值：Infinity无穷大和NaN(0/0)非数字（但是是数字类型）
* Infinity和-Infinity：

```
通过isFinite（）判断是否有限大，如果是Infinity，返回false；这里Infinity可以作为参数赋值给变量（比较大小的问题）

```
* NaN：

```
代表非数字的特殊数值，该属性用于指示某个值不是数字；

NaN的两个特点：（NaN == not a number）

1：任何涉及NaN的操作都会返回NaN；

2：NaN与任何数值都不相等，包括他自身；

不能与Number.NaN比较来检测一个值是不是数字，而只能调用isNaN()来比较；

isNaN（）（可以用来判断一个输入的值是不是数字）函数如果x是特殊的非数字NaN（或者能被转换为这样的值），返回的值就是true，如果x是其他值，则返回false。

```

##### 2：字符串（string）：
* 多个字符的有序序列；双引号和单引号引起来的都是字符串；

##### 3：布尔值（boolean）：true / false；

##### 4：undefind
* 如果使用一个未定义的变量，或者是没有初始值的变量，都会得到undefind，
> undefined == null(true); undefined === null(false)

##### 5：null
*只有一个值null，如果变量的值是null，那么这个变量存在但是为空；
null表示尚未存在的对象，但是函数或方法返回的是对象，找不到该对象时，返回的是null

##### 6: symbol(ES6)

* ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型
* Symbol 值通过Symbol函数生成。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的 Symbol 类型。凡是属性名属于 Symbol 类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。

```
let s = Symbol();

typeof s
// "symbol"

```

## 复杂数据类型
##### 对象
* 属性和方法的集合

## JS数据类型的判断
#### 1、typeof
* 返回一个表示数据类型的字符串，返回结果包括：number、boolean、string、symbol、object、undefined、function等7种数据类型，但不能判断null、array等

```
typeof Symbol(); // symbol 有效
typeof ''; // string 有效
typeof 1; // number 有效
typeof true; //boolean 有效
typeof undefined; //undefined 有效
typeof new Function(); // function 有效
typeof null; //object 无效
typeof [] ; //object 无效
typeof new Date(); //object 无效
typeof new RegExp(); //object 无效
```
#### 2、instanceof
* 用来判断A是否为B的实例，A instanceof B， 返回 boolean 值。instanceof 用来测试一个对象在其原型链中是否存在一个构造函数的 prototype 属性，但它不能检测 null 和 undefined

```
[] instanceof Array; //true
{} instanceof Object;//true
new Date() instanceof Date;//true
new RegExp() instanceof RegExp//true
null instanceof Null//报错
undefined instanceof undefined//报错
```
#### 3、Object.prototype.toString.call()
* 一般数据类型都能够判断，最准确最常用的一种

```
    Object.prototype.toString.call('') ;   // [object String]
    Object.prototype.toString.call(1) ;    // [object Number]
    Object.prototype.toString.call(true) ; // [object Boolean]
    Object.prototype.toString.call(undefined) ; // [object Undefined]
    Object.prototype.toString.call(null) ; // [object Null]
    Object.prototype.toString.call(new Function()) ; // [object Function]
    Object.prototype.toString.call(new Date()) ; // [object Date]
    Object.prototype.toString.call([]) ; // [object Array]
    Object.prototype.toString.call(new RegExp()) ; // [object RegExp]
    Object.prototype.toString.call(new Error()) ; // [object Error]			
```

# 变量
## 变量声明
* 1、遵循原则：先声明，后使用
* 2、预解析机制（变量提升）：对紧跟在关键字（如var，function）后面的变量名称进行声明提前（把声明部分提前，赋值部分保留在原位置）。遇到关键字就有声明提前。
## 变量作用域
* 1、全局作用域---全局变量：(ES5中)三种声明方式
* 2、作用域链的最顶层是window
> A．var 变量;
>> B．变量;
>>> C．windw.变量（原理：对象.属性）

区别:加var的变量，不能被delete删除，不加var的变量会被delete删除。
## 函数作用域---局部变量:
* 只有变量在函数内声明时，它才是局部变量
* 特例：不加var的变量在函数内声明，则是全局变量
* 加了var的变量在函数内声明，才是局部变量

## 变量的定义没有块级作用域(es5)
* （如：if，while等块中，即非函数的块），故里面声明的变量还是全局变量

## 块级作用域(es6)
* let定义的变量，只能在块作用域里访问，不能跨块访问，也不能跨函数访问。
* const用来定义常量，使用时必须初始化(即必须赋值)，只能在块作用域里访问，而且不能修改。对象是引用类型（const定义的对象引用能被修改）