title: css-centering
date: 2017-02-18 20:26:34
tags:
---
CSS居中总结：CSS居中是任何一个前端开发者必备的基础技能，实现居中不算很有技术难度的事情，但能实现居中的方式实在是太多了，这里对各种居中方法做一个总结，毕竟温故而知新嘛！

### 一.水平居中
##### 1.inline or line-* 元素
在块级父元素内的行内元素可以通过设置 **text-align:center** 来进行水平居中。

```css
div {
    margin: 10px;
}
.parent {
    width: 200px;
    height: 50px;
    text-align: center;
    border: 1px solid #000000;
}
```

```html
<div class="parent">水平居中</div>
```
![pic_1](http://o7bp9e1ec.bkt.clouddn.com/1488720138086)

```css
nav {
    margin: 10px;
    text-align: center;
    padding: 10px;
    border: 1px solid #000000;
}
nav a {
    text-decoration: none;
    background: #333;
    border-radius: 5px;
    color: white;
    padding: 3px 8px;
}
```

```html 
<nav role='navigation'>
    <a href="#0">One</a>
    <a href="#0">Two</a>
    <a href="#0">Three</a>
    <a href="#0">Four</a>
</nav>
```
![pic_2](http://o7bp9e1ec.bkt.clouddn.com/1488720502935)

##### 2.块级元素
如果该块级元素有具体的 width，可以通过设置块级元素的 **margin-left** 和 **margin-right** 的值为 **auto** 来居中。
```css
.main {
    background: white;
    margin: 20px 0;
    padding: 10px;
    border: 1px solid red;
}
.center {
    margin: 0 auto;
    width: 200px;
    padding: 20px;
    color: #000000;
    border: 1px solid #000000;
}
```

```html
<div class="main">
    <div class="center">
    I'm a block level element and am centered.
    </div>
</div>
```
![pic_3](http://o7bp9e1ec.bkt.clouddn.com/1488721052778)

##### 3.多个块级元素
如果你需要把两个或两个以上的块级元素在一行水平居中，你需要把这些块级元素的 **display** 设置为 **inline-block**，或者使用 **flex** 布局。

设置 display，**需设置块级元素的宽度**
```css
.inline-block-center {
    text-align: center;
    border: 1px solid red;
}
.inline-block-center div {
    max-width: 125px;
    display: inline-block;
    text-align: left;
    border: 1px solid #000000;
}
```

```html
<div class="inline-block-center">
    <div>
    I'm an element that is block-like with my siblings and we're centered in a row.
    </div>
    <div>
    I'm an element that is block-like with my siblings and we're centered in a row. I have more content in me than my siblings do.
    </div>
    <div>
    I'm an element that is block-like with my siblings and we're centered in a row.
    </div>
</div>
```
![pic_4](http://o7bp9e1ec.bkt.clouddn.com/1488722458999)

使用 flex 布局
```css
.flex-center {
    display: flex;
    justify-content: center;
    border: 1px solid red;
}
.flex-center div {
    border: 1px solid #000000;
}
```

```html
<div class="flex-center">
    <div>
    I'm an element that is block-like with my siblings and we're centered in a row.
    </div>
    <div>
    I'm an element that is block-like with my siblings and we're centered in a row. I have more content in me than my siblings do.
    </div>
    <div>
    I'm an element that is block-like with my siblings and we're centered in a row.
    </div>
</div>
```
![pic_5](http://o7bp9e1ec.bkt.clouddn.com/1488722803508)

### 二.垂直居中
##### 1.inline or line-* 元素
单行   
(1).设置相同的 padding-top 和 padding-bottom 值。
```css
.single {
    margin: 20px 0;
    padding: 50px;
    border: 1px solid red;
}

.single a {
    background: black;
    color: white;
    padding: 40px 30px;
    text-decoration: none;
    border: 1px solid #000000;
}
```

```html
<div class="single">
    <a href="#0">We're</a>
    <a href="#0">Centered</a>
    <a href="#0">Bits of</a>
    <a href="#0"></a>
</div>
```
![pic_6](http://o7bp9e1ec.bkt.clouddn.com/1488723144293)

(2).设置 line-height 与 父元素 height 相等
```css
.single-lineheight {
    background: white;
    margin: 20px 0;
    padding: 40px;
    border: 1px solid red;
}
.single-lineheight div {
    color: black;
    height: 100px;
    line-height: 100px;
    padding: 20px;
    width: 50%;
    white-space: nowrap;
    border: 1px solid #000000;
}
```

```html
<div class="single-lineheight">
    <div>
    I'm a centered line.
    </div>
</div>
```
![pic_7](http://o7bp9e1ec.bkt.clouddn.com/1488723707299)

多行   
flex 布局
```css
.flex-center-more {
    width: 240px;
    margin: 20px;
    color: #000000;
    display: flex;
    flex-direction: column;
    justify-content: center;
    height: 200px;
    overflow: auto;
    border: 1px solid red;
}
.flex-center-more p {
    margin: 0;
    padding: 20px;
    border: 1px solid #000000;
}
```

```html
<div class="flex-center-more">
    <p>I'm vertically centered multiple lines of text in a flexbox container.</p>
</div>
```
![pic_8](http://o7bp9e1ec.bkt.clouddn.com/1488724047544)

