title: javascript-array-reduce
date: 2017-03-07 09:19:46
tags: javascript | array | method
---
Javascript中，数据类型Array有一些非常实用而强大的原生方法，接下来对主要的四种方法：forEach, map, filter, reduce做一个使用总结，由于reduce方法用的少，而且该方法本身存在难点，所以会着重介绍reduce方法。

### Array四大迭代利器
#### 1.forEach()   
forEach()方法接受一个回调函数。如果没有抛出异常，数组中的每个元素都将会执行一次该函数。   

**语法**
```javascript
arr.forEach(function callback(currentValue, index, array) {
    //your iterator
}[, thisArg]);
```
**参数**   

| callback | 为每个元素执行的函数，接受三个参数 |
| --- | --- |
| currentValue | 数组中当前被处理的元素 |
| index | 当前元素的索引 |
| array | forEach()方法应用的数组 |
| thisArg | (可选)执行回调时使用this（即引用对象）的值 |
| 返回值 | undefined |

**注意点**   
forEach()将要处理的元素在callback函数第一次执行前就已经确定，所以在forEach()开始执行后添加到数组中的元素将不会被callback处理。   
如果现有元素的值发生了改变，传到callback里的值是forEach()取到的值。   
在取值前被删除的元素将不会被访问。如果被访问过的元素被删除了，之后的元素会被略过（索引发生了变化）。   
没有办法停止或打断forEach()循环，除了抛出异常。

#### 2.map()
map()方法会返回一个由提供的回调函数作用于数组中的每个元素后产生的新数组，“纯”方法，不会污染原数组。   

**语法**
```javascript
var new_array = arr.map(callback[, thisArg]);
```
**参数**   

| callback | 产生新数组的函数，接受三个参数 |
| --- | --- |
| currentValue | 数组中当前被处理的元素 |
| index | 当前元素的索引 |
| array | forEach()方法应用的数组 |
| thisArg | (可选)执行回调时使用this（即引用对象）的值 |
| 返回值 | 回调函数产生的新数组 |

**Examples**
```javascript
// 字符串中每个字符的字符码
var map = Array.prototype.map;
var a = map.call('string', function(c) {
    return c.charCodeAt(0);
});
```
```javascript
// 反转字符串
var str = '12345';
Array.prototype.map.call(str, function(c) {
    return c;
}).reverse().join('');
```
```javascript
// 字符串转整型
['1', '2', '3'].map(Number);
```

#### 3.filter()
filter()方法返回一个由提供的回调函数将数组中的每个元素过滤后组成的新数组

**语法**   
```javascript
var newArray = arr.filter(callback[, thisArg]);
```
**参数**   

| callback | 用来检测数组中的每个元素，返回true保留元素，false不保留，接受三个参数 |
| --- | --- |
| element | 数组中当前被处理的元素 |
| index | 当前元素的索引 |
| array | 被过滤的数组 |
| thisArg | (可选)执行回调时使用this（即引用对象）的值 |
| 返回值 | 满足回调函数的新数组 |

**Examples**
```javascript
// 筛选掉JSON数组中不满足条件的元素
var arr = [
    {id: 15},
    {id: -1},
    {id: 0},
    {id: 3},
    {id: 12.2},
    {},
    {id: null},
    {id: NaN},
    {id: 'undefined'}
];

var invalidEntries = 0;
function isNumber(obj) {
    return obj !== undefined && typeof(obj) === 'number' && !isNaN(obj);
}
function filterByID(item) {
    if(isNumber(item.id)) {
        return true;
    }
    invalidEntries++;
    return false;
}

var arrByID = arr.filter(filterByID);
```
```javascript
// 数组元素查询
var fruits = ['apple', 'banana', 'grapes', 'mango', 'orange'];
function filterItems(query) {
    return query.filter(function(el) {
        return el.toLowerCase().indexOf(query.toLowerCase()) > -1;
    });
}
```

#### 4.reduce()
**官方定义：**The reduce() method applies a function against an accumulator and each value of the array (from left-to-right) to reduce it to a single value.   

**语法**   
```javascript
arr.reduce(callback, [initialValue]);
```
**参数**   

| callback | 作用于数组中每个元素的方法，接受四个参数 |
| --- | --- |
| accumulator | 作为每次迭代的初始值，同时也作为上一次迭代的结果值，如果是第一次执行callback，并且给了initialValue，则为initialValue的值，否则为数组第一个元素的值 |
| currentValue | 数组中当前被处理的元素 |
| currentIndex | 当前元素的索引，如果给了initialValue，索引从0开始，否则从1开始 |
| array | reduce的数组 |
| initialValue | (可选)callback第一次调用时使用的第一个值，即初始值 |
| 返回值 | 返回最终的结果 |

**描述**
reduce()执行一个接受四个参数的回调函数。回调函数第一次调用时，如果有initialValue，accumulator的值为initialValue，currentValue的值为数组第一个元素的值。如果没有设置initialValue，accumulator的值为数组第一个元素的值，currentValue的值为数组第二个元素的值。   
**Note** 如果没有提供initialValue，reduce将会从索引1开始执行callback，略过第一个索引。如果提供了，从索引0开始。   

如果数组是空的，并且没有提供initialValue，将会抛出**TyoeError**。如果数组只有一个元素并且没有提供initialValue，或者数组是空的但提供了initialValue，reduce将会返回这一个孤独的值而不调用callback。   

**Examples**   
```javascript
// 数组扁平化
var flattened = [[0, 1], [2, 3], [4, 5]].reduce(
  function(a, b) {
    return a.concat(b);
  },
  []
);
// flattened is [0, 1, 2, 3, 4, 5]
```
```javascript
// 统计数组中的值的种类
var names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];

var countedNames = names.reduce(function (allNames, name) { 
  if (name in allNames) {
    allNames[name]++;
  }
  else {
    allNames[name] = 1;
  }
  return allNames;
}, {});
// countedNames is:
// { 'Alice': 2, 'Bob': 1, 'Tiff': 1, 'Bruce': 1 }
```
```javascript
// 取出数组中的所有对象里的某一个属性的值，并返回一个包含这些值的新数组
// friends - an array of objects 
// where object field "books" - list of favorite books 
var friends = [{
  name: 'Anna',
  books: ['Bible', 'Harry Potter'],
  age: 21
}, {
  name: 'Bob',
  books: ['War and peace', 'Romeo and Juliet'],
  age: 26
}, {
  name: 'Alice',
  books: ['The Lord of the Rings', 'The Shining'],
  age: 18
}];

// allbooks - list which will contain all friends books +  
// additional list contained in initialValue
var allbooks = friends.reduce(function(prev, curr) {
  return [...prev, ...curr.books];
}, ['Alphabet']);

// allbooks = [
//   'Alphabet', 'Bible', 'Harry Potter', 'War and peace', 
//   'Romeo and Juliet', 'The Lord of the Rings',
//   'The Shining'
// ]
```