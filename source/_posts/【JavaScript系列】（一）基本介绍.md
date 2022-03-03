---
title: 【JavaScript系列】（一）基本介绍
date: 2022-02-18 16:07:58
tags:
  - JacaScript
  - 编程语言
  - 前端
categories: 计算机
---

# 【JavaScript 系列】（一）基本介绍

## 什么是 JavaScript

JavaScript 最初被创建的目的是“使网页更生动”。
这种编程语言写出来的程序被称为**脚本**。它们可以被直接写在网页的 HTML 中，在页面加载的时候自动执行。
脚本以纯文本的形式提供和执行。它们不需要特殊的准备或编译即可运行。

## 浏览器中的 JavaScript 能做什么

现代的 JavaScript 是一种“安全的”编程语言。它不提供对内存或 CPU 的底层访问，因为它最初是为浏览器创建的，不需要这些功能。
JavaScript 的能力很大程度上取决于它运行的环境。例如，Node.js 支持允许 JavaScript 读取、写入任意文件，执行网络请求等的函数。
浏览器中的 JavaScript 可以做与网页操作、用户交互和 Web 服务器相关的所有事情。

## 浏览器中的 JavaScript 不能做什么

为了用户的（信息）安全，在浏览器中的 JavaScript 的能力是受限的。目的是防止恶意网页获取用户私人信息或损坏用户数据。

## 是什么使 JavaScript 与众不同

至少有三点是值得一提的：

- 与 HTML/CSS 完全集成
- 简单的事，简单地完成
- 被所有的主流浏览器支持，并且默认开启

## JavaScript 的“上层”语言

最近出现了许多新语言，这些语言在浏览器中执行之前，都会被**编译**（转化）成 JavaScript。
现代化的工具使得编译速度非常快且透明，实际上允许开发者使用另一种语言编写代码并会将其“自动转化”为 JavaScript。
此类语言的实例有：

- CoffeeScript
- TypeScript
- Flow
- Dart
- Brython
- Kotlin

> 本系列为笔者在自学 JavaScript 过程中的笔记，具体可访问[现代 JavaScript 教程](https://zh.javascript.info/)，这个教程写的真不错，很详细。笔者的博客可以当成这个教程的精简版，若有不太详细的地方可访问教程具体查看，若有错误的地方可去本博客托管的[github 仓库](https://github.com/transparent-reid/MyBlog)下提 issue。
