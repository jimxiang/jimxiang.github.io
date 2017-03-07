title: javascript-array-reduce
date: 2017-03-07 09:19:46
tags: javascript | array | method
---
Javascript中，数据类型Array有一些非常实用而强大的原生方法，接下来对主要的四种方法：forEach, map, fliter, reduce做一个使用总结，由于reduce方法用的少，而且该方法本身存在难点，所以会着重介绍reduce方法。

### 一.Array四大迭代利器
#### 1.forEach()   
forEach()方法接受一个回调函数。如果没有抛出异常，数组中的每个元素都将会执行一次该函数。   

**语法**
```javascript
arr.forEach(function callback(currentValue, index, array) {
    //your iterator
}[, thisArg]);
```
**参数**   
callback|为每个元素执行的函数，接受三个参数
-|-
currentValue|数组中当前处理的元素
index|当前元素的索引
array|forEach()方法应用的数组
thisArg|(可选)执行回调时使用此值（即引用对象）的值
返回值|undefined

**注意点**   
forEach()将要处理的元素在callback函数第一次执行前就已经确定，所以在forEach()开始执行后添加到数组中的元素将不会被callback处理。   
如果现有元素的值发生了改变，传到callback里的值是forEach()取到的值。   
在取值前被删除的元素将不会被访问。如果被访问过的元素被删除了，之后的元素会被略过（索引发生了变化）。   
没有办法停止或打断forEach()循环，除了抛出异常。

#### 2.map
map()方法会返回一个由提供的回调函数作用于数组中的每个元素后产生的新数组，“纯”方法，不会污染原数组。   

**语法**
```javascript
var new_array = arr.map(callback[, thisArg]);
```
**参数**
callback|产生新数组的函数，接受三个参数
-|-
currentValue|数组中当前处理的元素
index|当前元素的索引
array|forEach()方法应用的数组
thisArg|(可选)执行回调时使用此值（即引用对象）的值
返回值|回调函数产生的新数组

**Examples**
```javascript
var map = Array.prototype.map;
var a = map.call('string', function(c) {
    return c.charCodeAt(0);
});
```