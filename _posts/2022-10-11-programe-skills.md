---
layout: article
title: C++工程技巧
tags: 编程 C++
key: ICE-BA1
category: 论文
date: 2022-10-11 12:06:43
modify_date: 2022-10-11 12:06:48
typora-root-url: ..
---

1. C++工程的debug方法
2. C++程序性能分析方法

<!--more-->

## C++工程Debug方法

### 常规方法
通过Debug编译，将`CMAKE_BUILD_TYPE`设置为`Debug`，关闭编译优化。然而这样做最大的问题是程序运行会很慢，调试不方便。

### 改进方法
1. 将`CMAKE_BUILD_TYPE`设置为`RelWithDebInfo`
2. 将待调试的代码块关闭编译优化：
  ```c++
  #pragma GCC push_options
  #pragma GCC optimize("O0")
  {
    // debug code block
  }
  #pragma GCC pop_options
  ```
3. VSCode中进行debug配置, launch.json example:
  ```json
   {
     // Use IntelliSense to learn about possible attributes.
     // Hover to view descriptions of existing attributes.
     // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
     "version": "0.2.0",
     "configurations": [
         {
             "name": "(gdb) Launch",
             "type": "cppdbg",
             "request": "launch",
             "program": "[C++编译出的可执行exe文件路径]",
             "args": ["程序参数"],
             "stopAtEntry": false,
             "cwd": "${fileDirname}",
             "environment": [],
             "externalConsole": false,
             "MIMode": "gdb",
             "setupCommands": [
                 {
                     "description": "Enable pretty-printing for gdb",
                     "text": "-enable-pretty-printing",
                     "ignoreFailures": true
                 },
                 {
                     "description":  "Set Disassembly Flavor to Intel",
                     "text": "-gdb-set disassembly-flavor intel",
                     "ignoreFailures": true
                 }
             ]
         }
     ]
   }
  ```
4. 设置断点、编译、调试。可使用debug console查看局部变量。

## C++程序性能分析
gperftools(originally Google Performance Tools)包含了cpu性能分析工具，原理和gprof差不多，会在编译的时候插入为函数计时的代码。
另外gperftools中包含了heap profiling工具，可以对程序的内存占用情况进行分析。
使用方法：
1. 安装gperftools:
```shell
sudo apt-get install -y libtool gperf  libgoogle-perftools-dev
```
2. CmakeLists中添加编译选项
     - 添加-lprofiler用于CPU性能分析
     - 添加-ltcmalloc用于内存分析
4. 运行程序，会在运行目录下（roslaunch的运行目录是~/.ros）生成cputest.prof以及memtest.x.heap
5. 使用pprof命令可视化并分析数据
```shell
pprof [C++可执行文件路径] ./cpu_test.prof --svg > cpu_map_diff.svg
```

