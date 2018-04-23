# 函数声明(Function Declaration) VS 函数表达式(Function Expression)

这里主要讲一下函数声明和函数表达式的区别。

## 区别

### **函数声明（Function Declaration）- 在主程序流中作为独立的声明存在：**

#### 声明在全局作用域中

```javascript
// a.js
function foo () {
	...
}
```

#### 声明在函数作用域中

```javascript
function foo () {
	function bar () { // 函数声明，嵌套函数
		...
	}
}
```

### **函数表达式 （Function Expression）- 作为表达式的一部分或者其他语法结构的一部分存在：**

#### 作为表达式的一部分，例：

```javascript
// b.js
let foo = function () {}
```

#### 作为其他语法结构的一部分，例：

1、作为三目运算符的一部分

```javascript
true ? cosnole.log(1) : function foo () {}
foo // Uncaught ReferenceError: foo is not defined，此时该函数未声明，所以会报错
```

如果作为三目运算符的一部分时，`function foo () {}` 部分只有在引擎执行到该部分时才会运行，所以如果没有被执行到，`foo` 这个标识符是不存在的，使用会报错。

2、作为 `if-else` 语句的一部分：

```javascript
if (true) {
	function foo () {}
} else {
	function foo () {}
}
```

上面的代码等价于下面的：

```javascript
var foo
if (true) {
	foo = function foo () {}
} else {
	foo = function foo () {}
}
```

作为 `if-else` 语句的一部分时，不同于其在 `? :` 中的表现：在花括号中的函数声明一定会提升一个同名的标示 `foo` 到 `if-else` 的外层；而在 `? :` 结构中的部分是作为表达式存在的，一旦未执行，则直接丢掉，不会提升出同名标识符。

## 被执行时机

### 函数声明（Function Declaration）

#### 全局作用域

JS 引擎在执行整个脚本之前，会优先处理全局作用域中的函数声明，然后再处理全局作用域中的变量声明；如果变量名称与函数名称相同，则忽略该变量声明，如：

```javascript
function foo () {}

let foo;

typeof foo; // function

foo = 123; // line 4
```

如上所示，只有在执行到 `line 4` 这一行时，foo 才会被赋值为 `123`。

#### 函数作用域

函数作用域中的提升规则同全局作用域，区别是函数作用域中的声明提升发生在 JS 引擎开始执行函数第一行之前。

```javascript
function foo () {
	bar(); // line 1
	
	function bar () {
		...
	}
}

foo();
```
如上所示，在引擎执行 `line 1` 这行代码之前，会先执行 **提升**，当函数和变量都提升完之后，才会开始执行 `line 1` 这行代码。如果函数 `foo` 不被执行，则永远不会处理其函数体中的函数、变量等提升。

### 函数表达式（Function Expression）

函数表达式只有在 JS 引擎执行到其所在位置时才会被执行，例：

```javascript
foo(); // Uncaught TypeError: foo2 is not a function

...

var foo = function () {}; // line 2
```

上面的代码只会进行 变量 提升，只有在执行到 `line 2` 时才会将匿名函数赋值给变量 `foo`，所以通过函数表达式创建的函数不能在创建之前调用。

## 总结

> If the function is declared as a separate statement in the main code flow, that’s called a “Function Declaration”.
> 
> 如果函数是在主代码流中作为单独的结构声明的，则该函数是 “函数声明”。
> 
> If the function is created as a part of an expression, it’s called a “Function Expression”.
> 
> 如果是作为表达式的一部分创建的，则为 “函数表达式”。

## 参考

* [Function expressions and arrows](https://javascript.info/function-expressions-arrows)

## 作者 🦅

* [GitHub](https://github.com/Tao-Quixote)
* e-mail: <web.taox@gmail.com>
