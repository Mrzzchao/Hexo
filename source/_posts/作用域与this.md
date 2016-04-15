---
title: 作用域与this
date: 2016-04-08 15:30:03
categories: JavaScript
tags: this
toc: true
---

## 词法作用域
定义在词法阶段的作用域。简单来说就是函数，对象在定义时就决定好的执行范围,由代码书写的地方决定一切。


### 词法欺骗
但是，也可以通过一定的语法来改写这个先天决定的作用域。
- #### eval
接受的字符串参数就好像是书写在eval位置上的代码一样
```js
function foo(str, a) {
    eval( str ); // 欺骗！
    console.log( a, b );
}
var b = 2;
foo( "var b = 3;", 1 ); // 1, 3
```
<!--more-->

- #### with
会首先在with传入对象里面查询同名属性
```js
var obj = {
    a: 1,
    b: 2,
    c: 3
};
// 单调乏味的重复"obj"
obj.a = 2;
obj.b = 3;
obj.c = 4;
// 简单的快捷方式
with (obj) {
    a = 3;
    b = 4;
    c = 5;
}
```
> 注意：如果代码中大量使用eval(..)或with，那么运行起来一定会变得非常慢。无论引擎多聪明，试图将
这些悲观情况的副作用限制在最小范围内，也无法避免如果没有这些优化，代码会运行得更慢这个事实。

### 函数作用域
函数声明时就已决定的作用域。
#### 作用域图
![作用域图](http://7xrul1.com1.z0.glb.clouddn.com/%E4%BD%9C%E7%94%A8%E5%9F%9F2.png)
- 气泡1包含着整个全局作用域，其中只有一个标识符：foo。
- 气泡2包含着foo所创建的作用域，其中有三个标识符：a、bar和b。
- 气泡3包含着bar所创建的作用域，其中只有一个标识符：c。

__如果函数有嵌套，那被嵌套的函数可以引用上层函数作用域里的属性，反之不行__

![词法作用域](http://7xrul1.com1.z0.glb.clouddn.com/%E4%BD%9C%E7%94%A8%E5%9F%9F.png)

这个建筑代表程序中的嵌套作用域链。第一层楼代表当前的执行作用域，也就是你所处的位置。建筑的顶层代表全局作用域。<br>
LHS和RHS引用都会在当前楼层进行查找，如果没有找到，就会坐电梯前往上一层楼，如果还是没
有找到就继续向上，以此类推。一旦抵达顶层（全局作用域），可能找到了你所需的变量，也可能没找到，但无论如何查找过程都将停止。

> 注意：LHS在编译阶段，RHS在执行阶段

### 块作用域
很多语言（例如Java,C,C++）都有块作用域,但是JavaScript没有这个作用域模式
```js
function a() {
    var i = 5;
    for(var i = 0; i < 1; i++) {
        console.log(i);
    }
}
var b = a(); // 1
console.log(b.i) // 1
```
> 如果按块作用域来看，最后一段代码应该输出5，但是结果却是1，这是因为for循环的的 i 污染了全局里面的 i 然后让他重新赋值为0，最后循环结束就变为了1

#### 模拟块作用域(ES5以前)
- with

    用with从对象中创建出的作用域仅在with声明中而非外部作用域中有效。
- try/catch
```js
try {
    undefined(); // 执行一个非法操作来强制制造一个异常
}
catch (err) {
    console.log( err ); // 能够正常执行！
}
console.log( err ); // ReferenceError: err not found
```
外部无法访问内部定义的err

#### ES6
- ##### let

    let关键字可以将变量绑定到所在的任意作用域中（通常是{ .. }内部）。换句话说，let为其声明的
    变量隐式地了所在的块作用域。
```js
var foo = true;
if (foo) {
    let bar = foo * 2;
    bar = something( bar );
    console.log( bar );
}
console.log( bar ); // ReferenceError
```
- ##### const
    除了__let__以外，ES6还引入了__const__，同样可以用来创建块作用域变量，但其值是固定的（常量）。之后
    任何试图修改值的操作都会引起错误。
```js
var foo = true;
if (foo) {
    var a = 2;
    const b = 3; // 包含在if中的块作用域常
    a = 3; // 正常!
    b = 4; // 错误!
}
console.log( a ); // 3
console.log( b ); // ReferenceError!
```

## 动态作用域

什么是动态作用域？<br>
动态作用域就如你所想的就是下面这段代码发生的情况一样

```js
function foo() {
    console.log( a ); // 2
}
function bar() {
    var a = 3;
    foo();
}
var a = 2;
bar();
```

但是结果并不是这样
```js
function foo() {
    console.log( a ); // 3（ 不是2！）
}
function bar() {
    var a = 3;
    foo();
}
var a = 2;
bar();
```

__词法作用域关注函数在何处声明，而动态作用域关注函数从何处调用。__<br>
实际上JavaScript不具有动态作用域，他只有词法作用域。但是this机制从某种程度上很像动态作用域。

## This
this既不指向函数自身也不指向函数的词法作用域<br>
this实际上是在函数被调用时发生的绑定，它指向什么完全取决于函数在哪里被调用<br>
### 归纳来说this有四种绑定方式
- #### 默认绑定
在没有其他任何修饰的函数引用进行调用
```js
function foo() {
    console.log( this.a );
}
var a = 2;
foo(); // 2
```
 > this绑定了window

- #### 隐式绑定
```js
function foo() {
    console.log( this.a );
}
var obj = {
    a: 2,
    foo: foo
};
obj.foo(); // 2
```
 > this绑定了obj

而且对象属性引用链中只有最顶层或者说最后一层会影响调用位置。举例来说：
```js
function foo() {
    console.log( this.a );
}
var obj2 = {
    a: 42,
    foo: foo
};
var obj1 = {
    a: 2,
    obj2: obj2
};
obj1.obj2.foo(); // 42
```
 > this 绑定了obj2

但如果将属性引用传给一个变量后再调用，就会出现隐式丢失，变成默认绑定，例如：
```js
function foo() {
    console.log( this.a );
}
var obj = {
    a: 2,
    foo: foo
};
var bar = obj.foo; // 函数别名！
var a = "oops, global"; // a是全局对象的属性
bar(); // "oops, global"
```
 > this绑定了window

- #### 显示绑定
从this绑定的角度来说，call(..)和apply(..)是一样的，它们的区别体现在其他的参数上
     - call()
     - apply()
```js
function foo() {
    console.log( this.a );
}
var obj = {
    a:2
};
foo.call( obj ); // 2
```
 > this绑定了obj<br>
 __注意__:显示绑定会出现丢失绑定问题，也就是以后可以通过call,apply等再次修改this的绑定对象

- 硬绑定
```js
function foo() {
    console.log( this.a );
}
    var obj = {
    a:2
};
var bar = function() {
    foo.call( obj );
};
bar(); // 2
setTimeout( bar, 100 ); // 2
// 硬绑定的bar不可能再修改它的this
bar.call( window ); // 2
```
 > 通过对调用函数显示绑定的封装，使得bar.call实际上是绑定封装匿名函数的this，完全没影响到里面的foo绑定

- bind
```js
function foo(something) {
    console.log( this.a, something );
    return this.a + something;
}
var obj = {
    a:2
};
var bar = foo.bind( obj );
var b = bar( 3 ); // 2
console.log( b ); // 5
```
 > bind(..)会返回一个硬编码的新函数，它会把参数设置为this的上下文并调用原始函数

- #### new绑定
```js
function foo(a) {
    this.a = a;
}
var bar = new foo(2);
console.log( bar.a ); // 2
```
 > this绑定当前函数对象

### 四种绑定优先级（前高后低）
- new绑定
- 显示绑定
- 隐式绑定
- 默认绑定

#### 绑定例外
- 被忽略的this

    当call,apply,bind传入绑定参数为null,undefined时会被忽略，实际应用的是默认绑定
```js
function foo() {
    console.log( this.a );
}
var a = 2;
foo.call( null ); // 2
```
 > this绑定window

    - Object.create(null)
    > 不会创建Object.prototype委托，比{}更空,应该把Object.create(null)作为参数传入，避免传入null时，无意中使用默认绑定规则，导致的不可预计的后果

- 间接引用
```js
function foo() {
    console.log( this.a );
}
var a = 2;
var o = { a: 3, foo: foo };
var p = { a: 4 };
o.foo(); // 3
(p.foo = o.foo)(); // 2
```
 > this绑定了window,这里就好像把对象函数引用传过来在全局调用一样

- 软绑定
可以不顾优先级，任意进行绑定转换
- this词法
箭头函数

## 参考资料
- ### 《你不知道的JS》(真的写的很好)
