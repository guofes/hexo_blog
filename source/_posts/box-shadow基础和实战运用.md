title: box-shadow基础和实战运用
author: 郭峰
tags:
  - 前端基础
categories:
  - css
date: 2019-12-13 15:47:00
---
## 1.box-shadow定义与语法
* box-shadow阴影（外阴影与外发光）性向box添加一个或多个阴影。
### 语法
```css
box-shadow: offset-x offset-y blur spread color inset;
box-shadow: X轴偏移量 Y轴偏移量 [阴影模糊半径] [阴影扩展] [阴影颜色] [投影方式];
```
### 参数解释
* offset-x：必需，取值正负都可。offset-x水平阴影的位置。  
* offset-y：必需，取值正负都可。offset-y垂直阴影的位置。  
* blur:可选，只能取正值。blur-radius阴影模糊半径，0即无模糊效果，值越大阴影边缘越模糊。  
* spread：可选，取值正负都可。spread代表阴影的周长向四周扩展的尺寸，正值，阴影扩大，负值阴影缩小。  
* color: 可选。阴影的颜色。如果不设置，浏览器会取默认颜色，通常是黑色，但各浏览器默认颜色有差异，建议不要省略。可以是rgb(250,0,0)，也可以是有透明值的rgba(250,0,0,0.5)。   
* inset:可选。关键字，将外部投影(默认outset)改为内部投影。inset 阴影在背景之上，内容之下。
<!--more-->
### 浏览器支持
![浏览器支持](/images/pasted-0.png)
* -webkit-:  &emsp;10.0;  
* IE: &emsp; 9.0.0;  
* -moz:  &emsp;4.0 (2.0)[3] || 3.5(1.9.1)  
* -webkit: &emsp; 5.1[1] || 3.0  
* -o-: &emsp;10.5[1]   
说明：第一个数字表示支持该属性的第一个浏览器版本号，  
-webkit-, -ms- 或 -moz- 后的第二个数字为支持该前缀属性的第一个浏览器版本号。
## 案例
### 实现精彩365商品列表卡片半圆缺角效果
* 代码
```html
```
* 实现了，但是和阴影没有什么关系。。。。。  
[演示](https://guofes.github.io/learn/css/box_shadow/)