title: css 垂直水平居中
author: 郭峰
tags:
  - 前端基础
categories:
  - css
date: 2019-12-12 16:52:00
---
## 1.宽度已知
### 如下面所示要center垂直居中于wrapper
```css
// 公共代码
<div class="wrapper">
    <div class= "center">center</div>
</div>
<style>
.wrapper {
    border: 1px solid red;
    width: 300px;
    height: 300px;
}
.center {
    background: green;  
    width: 100px;
    height: 100px;
}

```
### 1.1 absolute + 负margin
```css
.wrapper {
    position: relative;
}
.center {
    position: absolute;
    top: 50%;
    left: 50%;
    margin-left: -50px;
    margin-top: -50px;
}
```
<!--more-->
### 1.2.text-align + line-height
仅适用于文字,且外层高度已知
```css
.wrapper{
     text-align: center;
     line-height: 150px;
   }
```
### 1.3.calc
```css
.center{
   width: 100px;
   height: 100px;
   margin-left: calc(50% - 50px);
   margin-top: calc(50% - 50px);
  }
```
### 1.4.absolute + calc
```css
.wrapper{
position: relative
}
.center{
	position: absolute;
   width: 100px;
   height: 100px;
   left: calc(50% - 50px);
   top: calc(50% - 50px);
  }
```


## 2.宽度未知
### 如下面所示要center垂直居中于wrapper
```css
// 公共代码
<div class="wrapper">
    <div class= "center">center</div>
</div>

```
### 2.1. flex布局
```css
.wrapper {
    display: flex;
    justify-content: center;
    align-items: center;
}
```
### 2.2.transform + absolute
这个组合，常用于图片的居中显示
```css
 .center {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
}
```
### 2.3.flex + margin
这是 flex 方法的变种。父级元素设置 flex，子元素设置 margin: auto;。可以理解为子元素被四周的 margin “挤” 到了中间

```css
.warpper {
	display:flex
}
 .center {
    margin: auto;
}
```
### 2.4.table-cell
利用 table 的单元格居中效果展示。好像也只适用于文字
```css
.wrapper {
    display: table;	
    text-align: center;
}
.center{
    display: table-cell;
    vertical-align: middle;
}
```
### 2.5.absolute + 四个方向的值相等
使用绝对定位布局，设置 margin:auto;，并设置 top、left、right、bottom 的 值相等即可（不一定要都是 0）。
```css
.warpper {
	position:relative;
}
 .center {
   position: absolute;
   left: 0;
   right: 0;
   top: 0;
   buttom: 0;
   margin: auto;
}
```
### 2.6.grid
像表格一样，网格布局让我们能够按行或列来对齐元素。 然而在布局上，网格比表格更可能做到或更简单。
```css
.wrapper {
    display: grid;
}

.center {
    align-self: center;
    justify-self: center;
}
```
### 2.7.::after（有问题）
伪元素也能用来实现居中么？感觉还是挺神奇的，
```css
    .wrapper{
        text-align: center;
    }
    .wrapper::after{
    content: '';
    display: inline-block;
    vertical-align: middle;
    }
    .center{
    vertical-align: middle;
    }
```
## 演示
[演示地址](https://guofes.github.io/learn/center/center.html)