---
layout: article
title: C++工程技巧
tags: 编程 C++
key: code3
category: 编程
date: 2022-10-11 12:06:43
modify_date: 2022-10-11 16:51:22
---

1. C++工程的debug方法
2. C++程序性能分析方法

<!--more-->

## C++工程Debug方法

### 常规方法

通过Debug编译，将`CMAKE_BUILD_TYPE`设置为`Debug`，关闭编译优化。然而这样做最大的问题是程序运行会很慢，调试不方便。
