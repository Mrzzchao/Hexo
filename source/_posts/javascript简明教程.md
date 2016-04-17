---
title: JavaScript基础知识点
date: 2016-03-20 15:30:03
categories: JavaScript
tags:
---

## 基本概念

###  数据类型
#### 简单数据类型
- __Undefined__
> 未经初始化或声明的变量

- Null
<!--more-->
- Boolean
- Number
- String

#### 复杂数据类型
- Object

###  操作符
- 一元操作符
- 位操作符
- 布尔操作符
- 乘性操作符
- 加性操作符
- 关系操作符
- 条件操作符
- 赋值操作符
- 逗号操作符

###  语句
- if 语句
- do-while 语句
- for 语句
- for-in 语句
- label 语句
- break 和 continue 语句
- __with 语句__
> 将代码的作用域设置到一个特定的对象中去

- switch 语句

###  函数
- __arguments__
> 函数参数集合

- __没用重载__
> 可通过检查传入参数的数目与类型而做出不同的反应来实现

## 变量、作用域和内存问题
###  基本类型和引用类型值
- 检测数据类型
> typeof

- 检测引用类型
> instanceof

###  执行环境及作用域￥
- __作用域链__
- 全局环境
    - 有 var 全局
    - 没 var 局部
- 局部环境
- 延长作用域链
    - try catch
    - with
- 没用块作用域
> if语句

- 垃圾收集
    - 标记清除（主流方式）
    - 引用计数
- 管理内存
> 手动释放不在引用的全局变量

## 引用类型
###  Object 类型
- 对象创建方式
    - new 创建
    - 字面量创建 （花括号{}）
- 属性引用
    - __.__ 引用（主流）
    - [] 引用（属性为变量或者含有空格）

###  Array 类型
- 检测数组
    - instanceof
    - isArray()
- 转换方法
    - toString
    - toLocaleString
    - valueOf
    - join
- 栈方法
    - push
    - pop
- 队列方法
    - shift
    - unshift
- 重排序方法
    - sort
    > 转化成字符串比较

    - reverse
- 操作方法
    - concat
    - slice
    > 取子数组

    - splice
      > 删除（2个参数）  删除、替换（三个参数）

- 位置方法
    - indexOf(从前)
    - lastIndexOf(从后)
- 迭代方法
    - every
    > 检查数组执行方法后每一项是否都返回true

    - filter
    > 选出数组执行方法后返回true的项

    - forEach
    > 数组中的每一项都执行方法

    - map
    > 返回数组每一项执行方法后返回的值

    - some
    > 检查数组执行方法后是否有一项返回true

    <table style="text-align:center">
        <thead>
            <th>第1个参数</th>
            <th>第2个参数</th>
            <th>第3个参数</th>
        </thead>
        <tbody>
            <tr>
                <td>数组项的值</td>
                <td>数组项的位置</td>
                <td>数组本身</td>
            </tr>
        </tbody>
    </table>

- 归并方法
    - reduce
    - reduceRight

    <table style="text-align:center">
        <thead>
            <th>第1个参数</th>
            <th>第2个参数</th>
            <th>第3个参数</th>
            <th>第4个参数</th>
        </thead>
        <tbody>
            <tr>
                <td>前一个值</td>
                <td>当前值</td>
                <td>当前项的位置</td>
                <td>数组本身</td>
            </tr>
        </tbody>
    </table>

###  Date 类型 @
- 继承的方法
- 日期格式化方法

###  RegExp 类型 @
- RegExp 实例属性
- RegExp 实例方法
- RegExp 构造函数属性
- 模式的局限性
<table style="text-align:center">
    <thead>
        <th>global 模式</th>
        <th>ignoreCase 模式</th>
        <th>multiline 模式</th>
    </thead>
    <tbody>
        <tr>
            <td>g</td>
            <td>i</td>
            <td>m</td>
        </tr>
        <tr>
            <td>表示全局</td>
            <td>表示不区分大小写</td>
            <td>表示多行模式</td>
        </tr>
    </tbody>
</table>

###  Function @
- 没有重载（深入理解）
> 因为函数名为指针，相同的函数名指向的为同一个函数

- 函数声明与函数表达式
    - 函数声明
    > 可以无视代码顺序

    - 函数表达式
    > 必须在表达式之后才可引用

- 作为值的函数
> 可以作为参数传递或返回，实际上就是个引用

- 函数内部属性

    __特殊对象__
    - arguments(也叫callee---指向拥有该arguments的函数)
    - this

- 函数的属性和方法

   #### 属性
   - length(命名参数数目)
   - prototype(所以实例方法的真正存在)

  #### 方法
   - apply(参数可不定)
   - call(参数确定)
   - bind

###  基本包装类型@
> 创建实例 <br>调用实力方法<br>销毁实例

- Booleadn 类型
- Number 类型
- String 类型
    - trim(去除字符串空格)

###  单体内置对象@
- Global 对象
    - eval(可把传入参数或字符串解析为js代码)
    - window（在浏览器中将global对象作为他的一部分来实现）
- Math 对象
