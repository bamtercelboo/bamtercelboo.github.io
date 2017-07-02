---
layout:     post
title:      "基于GCC的openMP学习与测试"
date:       2017-07-02
author:     "bamtercelboo"
header-img: "img/post-bg-2015.jpg"
tags:
    - 博客园
---

> <div>
  <a href="http://www.cnblogs.com/bamtercelboo/p/7107009.html">基于GCC的openMP学习与测试</a>
  </div>
<div>
  

- 随着CPU速度不再像以前那样显著提高，多核系统正变得越来越流行。为了利用这种能力，程序员在并行编程中变得很有知识变得越来越重要——让程序同时执行多个任务。Open Multiprocessing (OpenMP) 框架是一种功能极为强大的规范，可以帮助您利用 C、C++ 和 Fortran 应用程序中的多个核心带来的好处，是基于共享内存模式的一种并行编程模型, 使用十分方便, 只需要串行程序中加入OpenMP预处理指令, 就可以实现串行程序的并行化。
  

- 现在，openMP支持不同的编译器，GCC、Clang++、Solaris Studio、Intel C Compiler、Microsoft Visual C++等。程序员在编程时，只需要在特定的源代码片段的前面加入OpenMP专用的 #pargma omp 预编译指令，就可以“通知”编译器将该段程序自动进行并行化处理，并且在必要的时候加入线程同步及通信机制。当编译器选择忽略#pargma omp预处理指令时，或者编译器不支持OpenMP时，程序又退化为一般的通用串行程序，此时，代码依然可以正常运作，只是不能利用多线程和多核CPU来加速程序的执行而已。<a href="http://www.cnblogs.com/bamtercelboo/p/7107009.html">全文阅读</a>
<div>


