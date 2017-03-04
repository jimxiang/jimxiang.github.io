title: JavaScript学习笔记(1)
date: 2016-03-19 14:30:51
tags: JavaScript
---
##JavaScript中的apply(), call()和arguments对象   
>学习JavaScript，应该掌握函数式编程的特点和方法，为了做到这一点，详细理解函数调用和函数原型是非常有必要的。
打开浏览器，按F12打开浏览器控制台，选择console，让我们在console控制台里编写一些javascript代码来深入了解关于函数的一些知识。

###函数原型   
输入：

```javascript
Object.getOwnPropertyNames(Function.prototype);
```

得到：
```javascript
["length", "name", "arguments", "caller", "apply", "bind", "call", "toString", "constructor"]
```

这里的输出依赖于你使用的浏览器和JavaScript版本。以上属性里，我们将讨论以下这几个：
```javascript
Function.prototype.length
Function.prototype.call
Function.prototype.apply
```

首先，我们定义一个 "test" 函数：
```javascript
var test = function (a, b, c) {
    console.log({this: this, a: a, b: b, c: c});
}
```

这个函数简单记录了上下文变量(context)，即this的值，和输入参数的值。然后，我们输入不同的参数来调用这个函数：   

test('a');   
得到：

```javascript
Object { this: Window, a: "a", b: undefined, c: undefined }
```

test('this', 'is', 'cool');   
得到：

```javascript
Object { this: Window, a: "this", b: "is", c: "cool" }
```

>我们注意到，如果我们不输入第2、3个参数，浏览器将显示undefined。此外，我们注意到这个函数默认的上下文是全局对象Window。

###使用Function.prototype.call   
调用call函数时，需要把上下文变量this作为第一个输入的参数，然后传进其他参数。
*syntax:*
```javascript
function.call(this, arg1, arg2, ..., argn);
```

因此，下面这两行是等效的：

```javascript
test('this', 'is', 'cool');   
test.call(Window, 'this', 'is', 'cool');
```

###使用Function.prototype.apply   
函数apply比call更实用一些，和call类似，apply的调用方式也是把变量this设置为输入参数序列中的第一个参数的值，但输入参数序列的第二个参数也是最后一个，以数组（或者数组对象）的方式传入。
*Syntax:*

```javascript
function.apply(this, [arg1, arg2, ..., argn]);
```

因此，下面三行全部等效:   

```javascript
tester("this", "is", "cool");   
tester.call(window, "this", "is", "cool");   
tester.apply(window, ["this", "is", "cool"]);   
```

能够以数组的方式指定一个参数列表在多数时候非常有用（我们会发现这样做的好处的）。例如，Math.max是一个可变参数函数（一个函数可以接受任意数目的参数）。  

```javascript
Math.max(1,3,2); //=> 3   
Math.max(2,1); //=> 2
```

这样，如果我有一个数值数组，并且我需要利用Math.max函数找出其中最大的那个，我怎么用一行代码来做这个事儿呢？   

```javascript
var numbers = [3, 8, 7, 3, 1];   
Math.max.apply(null, numbers);   
//=> 8
```

###apply方法真正开始显示出它的重要是当配上特殊参数：Arguments对象。   
每个函数表达式在它的作用域中都有一个特殊的、可使用的局部变量：arguments。为了研究它的属性，让我们创建另一个test函数:

```javascript
var tester = function(a, b, c) {   
	console.log(Object.getOwnPropertyNames(arguments));   
};
```

>注：在这种情况下我们必须像上面这样使用Object.getOwnPropertyNames，因为arguments有一些属性没有标记为可以被枚举的，于是如果仅仅使用console.log(arguments)这种方式它们将不会被显示出来。   

现在我们按照老办法，通过调用test函数来测试下：

```javascript
test("a", "b", "c");
//=> ["0", "1", "2", "length", "callee"]

test.apply(null, ["a"]);
//=> ["0", "length", "callee"]
```

arguments变量的属性中包括了对应于传入函数的每个参数的属性，这些和.length属性、.callee属性没什么不同。
.callee属性提供了调用当前函数的函数的引用，但是这并不被所有的浏览器支持。就目前而言，我们忽略这个属性。
让我们重新定义一下我们的test函数，让它丰富一点：

```javascript
var tester = function() {
	console.log({
		'this': this,
		'arguments': arguments,
		'length': arguments.length
	});
};
tester.apply(null, ["a", "b", "c"]);
//=> { this: null, arguments: { 0: "a", 1: "b", 2: "c" }, length: 3 }
```

Arguments:是对象还是数组？
我们看得出，arguments完全不是一个数组，虽然多多少少有点像。在很多情况下，尽管不是，我们还是希望把它当作数组来处理。把arguments转换成一个数组，这有个非常不错的快捷小函数：

```javascript
	function toArray(args) {
	    return Array.prototype.slice.call(args);
	}

	var example = function(){
	    console.log(arguments);
	    console.log(toArray(arguments));
	};

	example("a", "b", "c");
	//=> { 0: "a", 1: "b", 2: "c" }
		//=> ["a", "b", "c"]
```

>这里我们利用Array.prototype.slice方法把类数组对象转换成数组。因为这个，在与.apply同时使用的时候arguments对象最终会极其有用。
