---
layout:     post
title:      "ubuntu、windows安装pytorch"
date:       2017-07-26
author:     "bamtercelboo"
header-img: "img/post-bg-2015.jpg"
tags:
    - 博客园
    - ubuntu
    - windows 
    - Pytorch
 
---

> <div>
  <a href="http://www.cnblogs.com/bamtercelboo/p/7074366.html">ubuntu、windows安装pytorch</a></div>


-  ubuntu安装pytorch查看博客园   （<a href="http://www.cnblogs.com/bamtercelboo/p/7074366.html">ubuntu、windows安装pytorch</a>）
-  
-  window安装与ubuntu安装几乎一致
-  
1. 安装Annconda3 windows版本（安装过程中一定要把环境变量加载，必须要勾选）
2. 还需要安装一些依赖库
   conda install numpy mkl setuptools cmake gcc cffi 
   conda install -c soumith magma-cuda75     # or magma-cuda80 if CUDA 8.0
3. conda install -c peterjc123 pytorch=0.1.12     windows运行这个命令就OK。
4. 安装结束之后，打开python输入import torch 若不出现错误就已经安装成功了。


