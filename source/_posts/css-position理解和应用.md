title: css position理解和应用
author: 郭峰
tags:
  - 前端基础
categories:
  - css
date: 2019-12-12 15:59:00
---
## 1.属性和意义
### 1.1定义
1、static：static是所有元素的默认属性，也就是可以理解为正常的文档流  
2、relative：relative是相对于自己文档的位置来定位的，对旁边的元素没有影响,不会脱离文档流  
3、absolute：是相对于父级非position:static 浏览器定位  
	&emsp;3.1如果没有任何一个父级元素是非position:static属性，则会相对于文档定位。  
	&emsp;3.2这里它的父级元素是包含爷爷级元素、祖爷爷级元素、祖宗级元素的。任意一级	&emsp;都可以。  
	&emsp;3.3如果它的父级元素和爷爷级元素都是非position:static 属性，则，它会选择距	&emsp;离最近	的父元素。  
4、fixed；相对于浏览器窗口来定位的。不会因为滚动条滚动  
5、stick:是css定位新增属性；可以说是相对定位relative和固定定位fixed的结合；它主要用在对scroll事件的监听上；简单来说，在滑动过程中，某个元素距离其父元素的距离达到sticky粘性定位的要求时(比如top：100px)；position:sticky这时的效果相当于fixed定位，固定到适当位置。
<!--more-->

### 1.2用法
1.static：默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）  
2.relative：生成相对定位的元素，相对于其正常位置进行定位。因此，”left:20” 会向元素的 LEFT 位置添加 20 像素  
3.absolute：生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。 
元素的位置通过left,top,right以及bottom属性进行规定  
4.fixed：生成绝对定位的元素，相对于浏览器窗口进行定位，素的位置通过left,top,right以及bottom属性进行规定  
5.stick:下面元素的距离达到sticky粘性定位的要求时(比如top：100px)；position:sticky这时的效果相当于fixed定位，固定到适当位置。
``` css
.div{
position: sticky;
top: 100px;
}
```
使用条件:  
&emsp;1、父元素不能overflow:hidden或者overflow:auto属性。  
&emsp;2、必须指定top、bottom、left、right4个值之一，否则只会处于相对定位  
&emsp;3、父元素的高度不能低于sticky元素的高度  
&emsp;4、sticky元素仅在其父元素内生效 
6.inherit：规定应该从父元素继承 position 属性的值。

## 案例
### 实现支付宝我的账单sticky效果
#### 代码
```html

```
#### 效果