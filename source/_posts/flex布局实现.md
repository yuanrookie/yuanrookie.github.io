---
title: flex布局实现及应用
author: yuansir
top: true
cover: true
toc: false
mathjax: false
summary: 通过复习flex布局的相关知识，并进行简单应用，以便在项目中更好的去运用flex布局
categories: flex
tags:
  - blog
  - hexo
abbrlink: 11
date: 2023-06-18 21:25:36
---
# flex布局详解及应用
## 一、flex布局知识点详细介绍
首先看完官方文档中flex布局的基本知识点[flex布局基本概念](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)
1. 子元素注意点
- flex-grow 是指项在 flex 容器中分配“剩余空间”的相对比例，默认为0
- flex-shrink 元素仅在默认宽度之和大于容器的时候才会发生收缩，其收缩的大小是依据 flex-shrink 的值,默认为1
- flex-basis 指定了 flex 元素在主轴方向上的初始大小(优先级高于width);如果没有分配尺寸，会采用元素内容的尺寸。
-  Flex 简写形式允许你把三个数值按这个顺序书写 — flex-grow，flex-shrink，flex-basis。
- flex: initial相当于0 1 auto;flex:auto 相当于1 1 auto;flex:none 相当于 0 0 auto;flex:1 相当于1 1 0 ;flex:2 相当于 2 1 0;
-   ---
- align-self: 用于对齐单个flex子项(stretch,flex-end,flex-start,center,baseline,auto)
- order: 指定单个项目的顺序，默认为0
2. 父元素注意点
- align-items:如果子元素没有定义高度，默认会在交叉轴方向拉伸到最高元素的高度。(stretch,flex-end,flex-start,center,baseline)
- justify-content:(flex-end,flex-start,center,space-between(元素之间间隔相等),space-around(每个元素的左右空间相等))
- align-content：flex 容器的 height 要大于 flex 项目的可视内容。然后它会将所有的 flex 项目打包成一块之后再对齐剩下的空间。(flex-end,flex-start,center,space-between(元素之间间隔相等),space-around(每个元素的左右空间相等),stretch)
- gap: 分为row-gap,column-gap 来控制每个子元素之间的间隔，默认为0
## 二、flex布局应用示例
1. 水平元素居中
```javaScript
  .triangle {
    border: 1px solid red;
    width: 500px;
    height: 400px;
    margin: 70px auto;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .d1 {
    width: 250px;
    height: 250px;
    background-color: pink;
    ;
  }
```
2. 实现圣杯布局（面从上到下，分成三部分：头部（header），躯干（body），尾部（footer）。其中躯干又水平分成三栏：从左到右为：导航、主栏、副栏）

```javaScript
   .grail {
    display: flex;
    flex-direction: column;
    align-items: stretch;
    text-align: center;
  }

  .grail div {
    flex: 1
  }

  .header,
  .footer {
    line-height: 100px;
    background-color: red;
  }

  .section {
    background-color: pink;
    display: flex;
  }

  .leftAside,
  .rightAside {
    background-color: blue;
    line-height: 400px;
  }

  .header,
  .footer,
  .leftAside,
  .rightAside {
    flex: 0 0 20% !important;
  }
```
   效果展示：
  ![圣杯布局](https://s2.loli.net/2023/06/21/AhzS6YfE7v2cFGL.png)
3. 双飞翼布局，就是两端固定宽高，中间自适应的三栏布局。

```javaScript
    .grail {
    display: flex;
    align-items: center;
    text-align: center;
    line-height: 400px;
  }

  .grail div {
    flex: 1
  }

  .leftAside,
  .rightAside {
    background-color: blue;
    flex: 0 0 200px !important;
  }

  .main {
    background-color: yellow;
    flex: 1
  }
```
效果展示：
![双飞翼布局效果图](https://s2.loli.net/2023/06/21/2AslX1C4gwGiVvY.png)
4. footer底部栏固定
```javaScript
  .grail {
    display: flex;
    align-items: stretch;
    flex-direction: column;
    text-align: center;
    min-height: 400px;
  }

  .main {
    background-color: yellow;
    flex: 1;
  }

  .header,
  .footer {
    background-color: red;
  }
```
效果展示：
![底部固定](https://s2.loli.net/2023/06/21/Qpes3LE6H1RxCay.png)
## 三、各类布局优缺点
例如：如何实现 高度已知，两端宽度固定，中间自适应？
1. flex布局
 优点：css3新特性，简单快捷，目前主流布局方式，解决旧特性定位时产生元素脱离文档流问题。
缺点：仅支持 IE9 以上浏览器。
解决方案：自适应div : flex:1
2. 绝对定位
优点：简单直接；
缺点：绝对定位同float布局一样会脱离文档流，高度塌陷问题。
出现高度塌陷问题，**可创建BFC来解决，**直接给父容器添加 overflow: auto; 或 hidden、scroll等。
3. float布局
优点：比较简单，兼容性好；
缺点：浮动会使元素脱离文档流，容易出现高度塌陷等问题，需做好清理浮动(BFC 块级格式化上下文)。
解决方式：通过创建BFC来解决这些问题
（1）float 除了none以外的值
（2）overflow 除了visible 以外的值（hidden，auto，scroll ）
（3）display (table-cell，table-caption，inline-block, flex, inline-flex)
（4）position值为（absolute，fixed）
（5）fieldset元素
4. Grid网格布局
 优点：可将网页划分成不同的网格，任意组合不同布局，可以实现以前只能通过诸如Bootstrapcss第三方框架的布局效果。
缺点：css 实验性新特性，在浏览器中还没有得到广泛的支持。
参考教程：[Grid详细讲解](https://link.csdn.net/?target=http%3A%2F%2Fwww.ruanyifeng.com%2Fblog%2F2019%2F03%2Fgrid-layout-tutorial.html)
