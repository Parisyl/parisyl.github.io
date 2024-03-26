---
title: ECMAScript 6 笔记
tags: [ECMAScript]
poster:
  topic: ES6 enhances JavaScript with new features like arrow functions and classes for better coding.
  headline: My ECMAScript 6 notes
  color: yellow
date: 2024-02-21 15:04:48
cover: https://f005.backblazeb2.com/file/img-forWeb/uPic/Y9y9bW.png
banner: https://f005.backblazeb2.com/file/img-forWeb/uPic/umqLFc.jpg
---

## 什么是 ECMAScript?
ECMAScript [ek - ma - script] 在中文中, ECMAScript 可以读作 "伊克玛Script"。
官方定义: ECMAScript 是定义脚本语言的规范, 而 JavaScript 是遵循 ECMAScript 规范实现的一种编程语言。
通俗说法: ECMAScript 好比是一本书的目录, 而 JavaScript 是这本书的具体内容。

### ES6 和 JavaScript 有什么区别？
ES6(ECMAScript 2015)是ECMAScript规范的第六个版本,而JavaScript是基于ECMAScript规范实现的编程语言, ES6可以被看作是 JavaScript 的一个重要的版本更新。
- ES6引入了"块级作用域",使用let和const关键字来声明变量和常量,使变量的作用域清晰可控。
- ES6引入了"箭头函数",箭头函数比传统的函数语法更简洁, 具有更少的冗余代码。
- ES6引入了"类(Class)"的概念,这是一种基于原型的面向对象编程的语法糖, 使用类可以更方便地创建和管理对象。
- ES6引入了"模板字符串", 使用反引号(\`)创建字符串可以方便地嵌入变量和表达式。
- ES6引入了"解构赋值", 这是一种新的赋值语法,可以将数组或对象的属性直接赋值给变量。
- ES6引入了"函数参数默认值"。
- ES6引入了"Promise对象", 简化了异步编程, 使其更可读和可维护。
- ES6引入了 Set、Map 等。
- ES6引入了"模块化"(ES Module)。
……

### ES6 ~ ES13 新特性
####  ES6(ECMAScript 2015)
- let和const关键字用于声明块级作用域变量和常量
- 箭头函数表达式
- 类定义和继承
- 模板字符串
- 解构赋值
- 函数参数默认值
- Promise 异步编程
- 异步函数 async/await
- Map 和 Set 数据结构
- 模块化 import 和 export
####  ES7(ECMAScript 2016)
- 数组 includes() 方法
- 指数运算符
- Array.prototype.includes()

#### ES8(ECMAScript 2017)
- async/await 异步编程解决方案的改进
- 共享内存和原子操作的支持
- Object.values() 和 Object.entries()
- String.prototype.padStart() 和 String.prototype.padEnd()

#### ES9(ECMAScript 2018)
- 异步迭代器
- Promise finally() 方法
- Rest/Spread 属性
- 正则表达式具有命名捕获组

#### ES10(ECMAScript 2019)
- Array.prototype.flat() 和 Array.prototype.flatMap()
- Object.fromEntries()
- String.prototype.trimStart() 和 String.prototype.trimEnd()
- catch 块可以省略参数

#### ES11(ECMAScript 2020)
- 可选链 ?. 和 Nullish 合并运算符 ??
- Promise.allSettled() 方法
- 动态 import()
- 全局对象globalThis

#### ES12(ECMAScript 2021)
- String.prototype.replaceAll()
- 数字分隔符
- WeakRefs 弱引用
- Promise.any() 方法

#### ES13(ECMAScript 2022)
- Class fields 类字段
- SIMD(Single Instruction, Multiple Data)指令集
- 更好的BigInt支持

## 变量和常量
### 什么是变量?
变量(Variable) 是用于存储数据的名称(标识符)，变量可以是任何类型, 如 "数值、字符串" 等。

- 字符串
姓名: 张三
网址: blog.peiong.com
- 整数
100
~~整数: 没有小数部分的数字, 包括 负数、零、正数~~ 
- 浮点数
3.14

let name = "张三"
let balance = 100
let PI = 3.14
~~ES6不区分整型和浮点型, 所有数字都使用 number类型 来表示~~ 

### 什么是常量?
常量(Constant) 是一个固定的值, 在程序运行中常量的值保持不变，常量通常用来表示不会改变的值, 如数学中的 π(圆周率) PI≈3.14159265359
const PI = 3.14

### 变量和常量有什么区别？
变量可以重新赋值。


