---
layout: post
keywords: blog
description: blog
title: "编写可维护的javascript（其实不仅仅是js）"
categories: [前端开发]
tags: [Archive]
group: archive
icon: file-o
---



<h2>编程风格</h2>
<h4>基本的格式化</h4>
<ul>
<li>js里面大括号的前半截应该紧跟上一行内容，这是由于ASI有时候会自动插入分号，在特殊情况下会对大括号在下一行的代码产生影响。</li>
<li>在以下内容间插入空行：每个流程语句之前，方法之间，方法的局部变量声明和第一条执行语句之间，注释之前，各种逻辑片段之间。</li>
<li>变量由名词开头，函数由动词开头，全是骆驼命名法。其中常见动词约定，can\has\is开头的函数返回一个布尔值，get返回一个非布尔值，set函数用来存储一个值。构造函数（类）则需要用帕斯卡命名法，名词开头。</li>
<li>建议字符串永远用双引号括起来而不使用obj.innerHTML = 'a href="#"'这种写法，即使里面嵌套了一层双引号，也应该使用转义\"。多行字符串可以在行末用加号连接。 </li>
<li>js是弱类型的，===表示不做动作直接比较，==表示转换为一种类型后比较。</li>
<li>undefined和null有区别，null是对象的占位符，undefined是等待被赋值的初始值。事实上，应该避免使用undefined。</li>
<li>避免显式地new出对象或数组再赋值，直接定义更加简洁和高效。</li>
</ul>


