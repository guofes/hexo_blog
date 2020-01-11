title: css性能提升
author: 郭峰
tags:
  - 前端基础
categories:
  - css
date: 2019-12-25 16:43:00
---
## 内联首屏关键CSS（Critical CSS）

* 首次有效绘制（First Meaningful Paint，简称FMP）即指页面的首要内容（primary content）出现在屏幕上的时间。这一指标影响用户看到页面前所需等待的时间，而**内联首屏关键CSS（即Critical CSS，可以称之为首屏关键CSS）**能减少这一时间。

* 将CSS直接内联到HTML文档中能使CSS更快速地下载。而使用外部CSS文件时，需要在HTML文档下载完成后才知道所要引用的CSS文件，然后才下载它们。所以说，内联CSS能够使浏览器开始页面渲染的时间提前，因为在HTML下载完成之后就能渲染

* 既然内联CSS能够使页面渲染的开始时间提前，那么是否可以内联所有的CSS呢？答案显然是否定的，这种方式并不适用于内联较大的CSS文件。因为初始拥塞窗口3存在限制（TCP相关概念，通常是 14.6kB，压缩后大小），如果内联CSS后的文件超出了这一限制，系统就需要在服务器和浏览器之间进行更多次的往返，这样并不能提前页面渲染时间。因此，我们应当只将渲染首屏内容所需的关键CSS内联到HTML中。

<!--more-->
* 既然已经知道内联首屏关键CSS能够优化性能了，那下一步就是如何确定首屏关键CSS了。显然，我们不需要手动确定哪些内容是首屏关键CSS。Github上有一个项目Critical CSS4，可以将属于首屏的关键样式提取出来，大家可以看一下该项目，结合自己的构建工具进行使用。当然为了保证正确，大家最好再亲自确认下提取出的内容是否有缺失。
* 不过内联CSS有一个缺点，内联之后的CSS不会进行缓存，每次都会重新下载。不过如上所说，如果我们将内联后的文件大小控制在了14.6kb以内，这似乎并不是什么大问题。

## 异步加载CSS
* CSS会阻塞渲染，在CSS文件请求、下载、解析完成之前，浏览器将不会渲染任何已处理的内容。有时，这种阻塞是必须的，因为我们并不希望在所需的CSS加载之前，浏览器就开始渲染页面。那么将首屏关键CSS内联后，剩余的CSS内容的阻塞渲染就不是必需的了，可以使用外部CSS，并且异步加载。
> 四种方式
* 使用JavaScript动态创建样式表link元素，并插入到DOM中

```
// 创建link标签
const myCSS = document.createElement( "link" );
myCSS.rel = "stylesheet";
myCSS.href = "mystyles.css";
// 插入到header的最后位置
document.head.insertBefore( myCSS, document.head.childNodes[ document.head.childNodes.length - 1 ].nextSibling );

```
* 将link元素的media属性设置为用户浏览器不匹配的媒体类型（或媒体查询），如media="print"，甚至可以是完全不存在的类型media="noexist",在文件加载完成之后，将media的值设为screen或all，从而让浏览器开始解析CSS。

```
<link rel="stylesheet" href="mystyles.css" media="noexist" onload="this.media='all'">

```
* 通过rel属性将link元素标记为alternate可选样式表，也能实现浏览器异步加载。同样别忘了加载完成之后，将rel改回去。

```
<link rel="alternate stylesheet" href="mystyles.css" onload="this.rel='stylesheet'">

```
上述的三种方法都较为古老。现在，rel="preload"5这一Web标准指出了如何异步加载资源，包括CSS类资源。

```
<link rel="preload" href="mystyles.css" as="style" onload="this.rel='stylesheet'">

```



## 文件压缩

* 文件的大小会直接影响浏览器的加载速度，这一点在网络较差时表现地尤为明显。相信大家都早已习惯对CSS进行压缩，现在的构建工具，如webpack、gulp/grunt、rollup等也都支持CSS压缩功能。压缩后的文件能够明显减小，可以大大降低了浏览器的加载时间。

## 去除无用CSS

* 手动删除这些无用CSS是很低效的。我们可以借助Uncss7库来进行。Uncss可以用来移除样式表中的无用CSS，并且支持多文件和JavaScript注入的CSS。

## 有选择地使用选择器

CSS选择器的匹配是从右向左进行的，这一策略导致了不同种类的选择器之间的性能也存在差异

* 保持简单，不要使用嵌套过多过于复杂的选择器。
* 通配符和属性选择器效率最低，需要匹配的元素最多，尽量避免使用。
* 不要使用类选择器和ID选择器修饰元素标签，如h3#markdown-content，这样多此一举，还会降低效率。
* 不要为了追求速度而放弃可读性与可维护性。

## 减少使用昂贵的属性
* 在浏览器绘制屏幕时，所有需要浏览器进行操作或计算的属性相对而言都需要花费更大的代价。当页面发生重绘时，它们会降低浏览器的渲染性能。所以在编写CSS时，我们应该尽量减少使用昂贵属性，如box-shadow/border-radius/filter/透明度/:nth-child等。

## 优化重排与重绘

### 减少重排

 重排会导致浏览器重新计算整个文档，重新构建渲染树，这一过程会降低浏览器的渲染速度,一下操作会是页面重排
 
* 改变font-size和font-family
* 改变元素的内外边距
* 通过JS改变CSS类
* 通过JS获取DOM元素的位置相关属性（如width/height/left等）
* CSS伪类激活
* 滚动滚动条或者改变窗口大小


### 避免不必要的重绘

* 当元素的外观（如color，background，visibility等属性）发生改变时，会触发重绘。在网站的使用过程中，重绘是无法避免的。浏览器对此做了优化，它会将多次的重排、重绘操作合并为一次执行。不过我们仍需要避免不必要的重绘，如页面滚动时触发的hover事件，可以在滚动的时候禁用hover事件，这样页面在滚动时会更加流畅。

## 不要使用@import

* 使用@import引入CSS会影响浏览器的并行下载
* 多个@import会导致下载顺序紊乱。在IE中，@import会引发资源文件的下载顺序被打乱，即排列在@import后面的js文件先于@import下载，并且打乱甚至破坏@import自身的并行下载。