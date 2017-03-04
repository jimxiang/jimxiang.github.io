title: javascript-methods
date: 2017-02-12 21:22:11
tags: javascript
---
Javascript 包含了少量用在标准类型上的标准方法。
---
## Array
### array.concat(item...)
concat方法返回一个新数组，它包含array的浅复制，，并将一个或多个参数 item 附加在其后。如果参数是一个数组，那么它的每个元素会被分别添加。
```javascript
var a = ['a', 'b', 'c'];
var b = ['x', 'y', 'z'];
var c = a.concat(b, true);
// c 是 ['a', 'b', 'c', 'x', 'y', 'z', true]
```

### array.join(separator)
join方法把一个 array 构造成一个字符串。它将 array 中的每个元素构造成一个字符串，并且用一个 separator 作为分隔符把它们连接在一起。默认的 separator 是 ','。为了实现无间隔的连接，我们可以使用空字符串作为 separator。   
如果你想把大量的片段组装成一个字符串，把这些片段放到一个数组中并用 join 方法连接它们通常比用 + 元素运算符连接这些片段要快。
```javascript
var a = ['a', 'b', 'c'];
var b = a.join('');
// b 是 'abc';
```

### array.pop()
pop 和 push 方法使数组 array 像堆栈一样工作。pop 移除 array 中的最后一个元素并返回该元素。如果 array 是空的，它会返回 undefined。
```javascript
var a = ['a', 'b', 'c'];
var b = a.pop();
// a 是 ['a', 'b'], b 是 'c'
```

### array.push(item...)
push 方法将一个或者多个参数 item 附加到一个数组的尾部。不像 concat 方法那样，它会修改数组 array，如果参数 item 是一个数组，它会将参数数组作为整个添加到数组中。它返回这个数组 array 的新长度值。
```
var a = ['a', 'b', 'c'];
var b = ['x', 'y', 'z'];
var c = a.push(b, true);
// a 是['a', 'b', 'c', ['x', 'y', 'z'], true], c 是 5
```

### array.reverse()
reverse 方法反转数组 array 中元素的顺序。它返回当前的 array
```javascript
var a = ['a', 'b', 'c'];
var b = a.reverse();
// a 和 b 都是 ['c', 'b', 'a']
```

### array.shift()
shift 方法移除数组 array 中的第一个元素。如果这个数组是空的，它会返回 undefined。shift 通常比 pop 慢得多。
```javascript
var a = ['a', 'b', 'c'];
var b = a.shift();
// a 是 ['b', 'c'], b 是 'a'
```

### array.slice(start, end)
slice 对 array 中的一段做浅复制。第一个被复制的元素是 array[start]，它将一直复制到 array[end]为止。end 参数是可选的，并且默认值是该数组的长度。如果两个参数中的任何一个是负数，array.length 将和它们相加起来试图使它们成为非负数。如果 start 大于等于 array.length，得到的结果将是一个新的空数组。
```javascript
var a = ['a', 'b', 'c'];
var b = a.slice(0, 1); // b 是 'a'
```

### array.sort()
sort 方法对 array 进行适当的排序，它不能正确给一组数字排序，因为该方法假定排序的元素是字符串，所以会把数字转换为字符串，从而数字数组排序会得到一个“错误”的结果。但可以使用自己的比较函数。
```javascript
var a = [10, 2, 4, 7];
// 从小到大排序
a.sort(function(a, b) {
    return a - b;
});
// a 是 [2, 4, 7, 10]

// 从大到小排序
a.sort(function(a, b) {
    return b - a;
});
// a 是 [10, 7, 4, 2]
```
上面的方法只能给数字排序，如果给任意简单值数组排序，则必须做更多的工作
```javascript
var a = ['aa', 'bb', 'd', 23, 12, 1, 45];
a.sort(function(a, b) {
    if(a === b) {
        return 0;
    }
    if(typeof a === typeof b) {
        return a < b ? -1 : 1;
    }
    return typeof a < typeof b ? -1 : 1;
});
// a 是 [1, 12, 23, 45, "aa", "bb", "d"]
```
给对象数组排序
```javascript
// by 函数接受一个成员名字符串作为参数
// 并返回一个可以用来对包含该成员的对象数组进行排序的比较函数
var by = function(name) {
    return function(o, p) {
        var a, b;
        if(typeof o === 'object' && typeof p === 'object' && o && p) {
            a = o[name];
            b = p[name];
            if(a === b) {
                return 0;
            }
            if(typeof a === typeof b) {
                return a < b ? -1 : 1;
            }
            return typeof a < typeof b ? -1 : 1;
        } else {
            throw {
                name: 'Error',
                message: 'Expected an object when sorting by ' + name
            };
        }
    };
}
var s = [
    {first: 'Joe', last: 'Besser'},
    {first: 'Moe', last: 'Howward'},
    {first: 'Joe', last: 'DeRita'},
    {first: 'Shemp', last: 'Howward'},
    {first: 'Larry', last: 'Fine'},
    {first: 'Currly', last: 'Howard'}
];
s.sort(by('first'));
/* s 是 
[
    {first: 'Currly', last: 'Howard'}
    {first: 'Joe', last: 'Besser'},
    {first: 'Joe', last: 'DeRita'},
    {first: 'Larry', last: 'Fine'},
    {first: 'Moe', last: 'Howward'},
    {first: 'Shemp', last: 'Howward'},
];
*／
```
基于多个键值排序，可以修改 by 函数，让其可以接受第二个参数，当主要的键值产生一个匹配的时候，另一个 compare 方法将被调用以决出高下。
```javascript
// by 函数接受一个成员名字符串和一个可选的次要比较函数作为参数，
// 并返回一个可以用来对包含该成员的对象数组进行排序的比较函数。
// 当 o[name] === p[name] 时，次要比较函数被用来决出高下
var by = function(name, minor) {
    return function(o, p) {
        var a, b;
        if(o && p && typeof o === 'object' && typeof p === 'object') {
            a = o[name];
            b = p[name];
            if(a === b) {
                return typeof minor === 'function' ? minor(o, p) : 0;
            }
            if(typeof a === typeof b) {
                return a < b ? -1 : 1;
            }
            return typeof a < typeof b ? -1 : 1;
        } else {
            throw {
                name: 'Error',
                message: 'Expected an object when sorting by ' + name
            };
        }
    }
}
var s = [
    {first: 'Joe', last: 'Besser'},
    {first: 'Moe', last: 'Howward'},
    {first: 'Joe', last: 'DeRita'},
    {first: 'Shemp', last: 'Howward'},
    {first: 'Larry', last: 'Fine'},
    {first: 'Currly', last: 'Howard'}
];
s.sort(by('last', by('first')));
/* s 是 
[
    {first: 'Joe', last: 'Besser'},
    {first: 'Joe', last: 'DeRita'},
    {first: 'Larry', last: 'Fine'},
    {first: 'Currly', last: 'Howard'}
    {first: 'Moe', last: 'Howward'},
    {first: 'Shemp', last: 'Howward'},
];
*／
```

### array.splice(start, deleteCount, item...)
splice 方法从 array 中移除 1 个或多个元素，并用新的 item 替换它们。参数 start 是从数组 array 中移除元素的开始位置。参数 deleteCount 是要移除元素的个数。如果有额外的参数那些 item 都将插入到所移除元素的位置上它返回一个包含被移除元素的数组。   
splice 最主要的用处是从一个数组中删除元素。千万不要与 slice 混淆，slice 主要的用处是对数组的一段做浅复制。

### array.unshift(item...)
unshift 方法像 push 方法一样用于将元素添加到数组中，但它是把元素插入到 array 的开始部分而不是尾部。它返回 array 的新的长度值。


## Function
### function.apply(thisArg, argArray)
apply 方法调用函数 function，传递一个将被绑定到 this 的对象和一个可选的参数数组。apply 方法被用在apply调用模式中。

## Number
### number.toExponential(fractionDigits)
toExponential 方法把这个 number 转换成一个指数形式的字符串。可选参数 fractionDigits 控制其小数点后的数字位数。它的值必须在 0 至 20 之间。

### number.toFixed(fractionDigits)
toFixed 方法把这个 number 转换成为一个十进制数形式的字符串。可选参数 fractionDigits 控制其小数点后的数字位数。它的值必须在 0 至 20 之间。默认为 0.

### number.toPrecision(precision)
toPrecision 方法把这个 number 转换成为一个十进制数形式的字符串。可选参数 precision 控制有效数字的位数。它的值必须在 0 至 21 之间。

### number.toString(radix)
toString 方法把这个 number 转换成为一个字符串。可选参数 radix 控制基数。它的值必须在 2 和 36 之间。默认的 radix 是以 10 为基数的。radix 参数最常用的是整数，但它可以用任意的数字。

## Object
### object.hadOwnProperty(name)
如果这个 object 包含了一个名为 name 的属性，那么这个 hasOwnProperty 方法返回 true。原型链中的同名属性是不会被检查的。

## RegExp
### regexp.exec(string)
exec 方法是使用正则表达式的最强大（和最慢）的方法。如果它成功地匹配 regexp 和字符串 string，它会返回一个数组。数组中下标为 0 的元素将包含正则表达式 regexp 匹配的子字符串。下标为 1 的元素是分组 1 捕获的文本，下标为 2 元素是分组 2 捕获的文本，以此类推。如果匹配失败，那么它会返回 null。   

如果 regexp 带有一个 g 标志（全剧标志），事情变得有点更加复杂了。查找不是从这个字符串的起始位置开始，而是从 regexp.lastIndex（它初始化为 0）位置开始。如果匹配成功，那么 regexp.lastIndex将被设置为该匹配后第一个字符串的位置。不成功的匹配会重置 regexp.lastIndex为 0。   

这就允许你通过在一个循环中调用 exec 去查询一个匹配模式在一个字符串中发生几次。有两件事情需要注意。如果你提前退出了这个循环，再次进入这个循环前必须把 regexp.lastIndex 重置到 0。^ 因子也仅匹配 regexp.lastIndex为 0的情况。

### regexp.test(string)
test 方法是使用正则表达式的最简单（和最快）的方法。如果该 regexp 匹配 string，它返回 true，否则，返回 false。不要对这个方法使用 g 标识。

## String
### string.charAt(pos)
charAt 方法返回在 string 中 pos 位置处的字符串。如果 pos 小于 0 或大于等于字符串的长度 string.length，它会返回空字符串。JavaScript 没有字符类型。这个方法返回的结果是一个字符串。

### string.charCodeAt(pos)
charCodeAt 方法同 charAt 一样，只不过它返回的不是一个字符串，而是以整数形式表示的在 string 中的 pos 位置处的字符串的字符码位。

### string.concat(string...)
concat 方法通过将其他的字符串连接在一起来构造一个新的字符串。它很少被使用，因为 + 运算符更为方便。

### string.indexOf(searchString, position)
concat 方法在 string 内查找另一个字符串 searchString。如果它被找到，则返回第一个匹配字符的位置，否则返回 -1。可选参数 position 可设置从 string 的某个指定的位置开始查找。

### string.lastIndexOf(searchString, position)
lastIndexOf 方法和 indexOf 方法类似，只不过它是从该字符串的末尾开始查找而不是从开头。

### string.localeCompare(that)
localeCompare 方法比较两个字符串。如何比较字符串的规则没有详细说明。如果 string 比字符串 that 小，那么结果为负数。如果它们是相等的，那么结果为0。这类似于 array.sort比较函数的约定。

未完。。。