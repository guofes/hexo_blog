title: BFC定义与原理
author: 郭峰
tags:
  - 前端基础
categories:
  - css
date: 2019-12-15 15:05:00
---
# BFC
* BFC（Block Formatting Context）块级格式化上下文，是Web页面中盒模型布局的CSS渲染模式，指一个独立的渲染区域或者说是一个隔离的独立容器。

# 形成BFC的条件
* 1、浮动元素，float 除 none 以外的值； 
* 2、定位元素，position（absolute，fixed）； 
* 3、display 为以下其中之一的值 inline-block，table-cell，table-caption； 
* 4、overflow 除了 visible 以外的值（hidden，auto，scroll）；

# BFC的特性
* 1.内部的Box会在垂直方向上一个接一个的放置。(对比IFC(行内格式化上下文)的特性，盒子在水平方向一个接着一个排列。)
* 2.垂直方向上的距离由margin决定
* 3.bfc的区域不会与float的元素区域重叠。
* 4.计算bfc的高度时，浮动元素也参与计算
* 5.bfc就是页面上的一个独立容器，容器里面的子元素不会影响外面元素。
<!--more-->

# 场景
### 特性2：
> 场景一：外边距折叠（margin collapse）,一是父子外边距叠加，二是兄弟外边距叠加
* 一个父盒子如果没有padding-top和border-top，这个父盒子的margin-top会和其内部文档流中的第一个子元素的margin-top重叠(父子div的margin重叠)形成BFC可解决

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>bfc</title>
    <style>
    .father_box{
        background: red;
        width: 300px;
        overflow: hidden;
        height: 300px;
    }
    .son_box{
        background: green;
        height: 150px;
        width: 300px;
        margin-top: 100px;
    }
    </style>
</head>
<body>
    <div class="father_box">
        <div class="son_box">

        </div>
    </div>
</body>
</html>

```
> 场景二：两栏布局（左边固定，右边自适应），三栏布局（中间自适应）
* bfc的区域不会与float的元素区域重叠 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>bfc</title>
    <style>
    .column{
        width: 100%;
        height: 200px;
    }
    .box1{
        float: left;
            width: 200px;
            height: 200px;
            margin-right: 10px;
            background-color: red;
    }
    .box2{
        overflow: hidden;/*创建bfc */
        height: 200px;
        background-color: purple;
    }
    </style>
</head>
<body>
    <div class="column">
        <div class="box1"></div>
        <div class="box2"></div>
    </div>
</body>
</html>

```
> 场景三  计算bfc的高度时，浮动元素也参与计算(利用overflow:hidden清除浮动,浮动的盒子无法撑出处于标准文档流的父盒子的height)

```html

    .float_height{
        background: #000;
        width: 100%;
        overflow: hidden;/*创建bfc */
    }
    .box3{
        height: 200px;
        width: 200px;
        float: left;
        background: #0c0;
    }
    <div class="float_height">
        <div class="box3"></div>
    </div>
```

## 演示
[演示地址](https://guofes.github.io/learn/css/bfc/index.html)