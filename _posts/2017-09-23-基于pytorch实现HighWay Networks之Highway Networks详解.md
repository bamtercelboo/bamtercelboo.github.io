---
layout:     post
title:      "基于pytorch实现Highway Networks之Highway Networks详解"
date:       2017-09-23
author:     "bamtercelboo"
header-img: "img/post-bg-2015.jpg"
tags:
    - 博客园
---


## （一）简述---承接上文---基于pytorch实现HighWay Networks之Train Deep Networks##

>上文已经介绍过Highway Netwotrks提出的目的就是解决深层神经网络训练困难的问题，以及简单的解释了为什么深层神经网络会出现梯度消失和梯度爆炸的问题，这里详细的介绍一些Highway Networks以及使用pytorch实现Highway Networks。


## （二）Highway Networks##

- **什么是Highway Networks?**
> Highway Netowrks是允许信息高速无阻碍的通过各层，它是从Long Short Term Memory(LSTM) recurrent networks中的gate机制受到启发，可以让信息无阻碍的通过许多层，达到训练深层神经网络的效果，使深层神经网络不在仅仅具有浅层神经网络的效果。

- **Notation**
> （.）操作代表的是矩阵按位相乘
> 
> sigmoid函数：sigmoid=  1/(1+e^(-x) )

- **Highway Networks formula**
> 普通的神经网络由L层组成，用H将输入的x转换成y,忽略bias。H是非线性激活函数，但是，通常呀可以采用其他的形式，像convolutional和recuerrent。

> ![](https://i.imgur.com/mZLjQcH.png)
> 
> 对于Highway Networks,增加了两个非线性转换层，T（transform gate） 和 C（carry gate），T表示输入信息被转换的部分，C表示的是原始信息x保留的部分 ，其中 T=sigmoid(wx + b) 
> 
> ![](https://i.imgur.com/GHOGFtH.png)
> 
> 为了计算方便，这里定义了 C =  1 - T
> 
> ![](https://i.imgur.com/BGkRdf3.png)
> 
> 需要注意的是x, y, H, T的维度必须一致,几个公式相比，公式3要比公式1灵活的多，可以考虑一下特殊的情况，T= 0的时候，y = x，原始信息全部保留，T = 1的时候，Y = H，原始信息全部转换，不在保留原始信息，仅仅相当于一个普通的神经网络。
> 
> ![](https://i.imgur.com/xXwlRys.png)
> 
> ![](https://i.imgur.com/C6sjdpM.png)
> 

- **搭建Highway Networks策略**
> 上文已经说过，x，y，H，T的维度必须是一致的，这里提供了两种策略：
> 
> 采用sub-sampling或者zero-padding(下采样或者是补零的操作)。
> 
> 使用普通的线性层改变维度，不使用Highway。

- **个人实验结果**
> 
> ![](https://i.imgur.com/59PxHT0.jpg)
> 
> 在相同的参数情况下测试了不同深度的神经网络对于情感分析5分类任务的准确率，从图中可以看出浅层神经网络对比变化不是很明显，5层的话就有了一些变化，准确率相差了一个点左右。由于硬件资源，更加深的深层神经网络还没有测试。

- **Paper 实验结果**
> ![](https://i.imgur.com/zOukeYJ.jpg)
> 
> 从论文的实验结果来看，当深层神经网络的层数能够达到50层甚至100层的时候，loss也能够下降的很快，犹如几层的神经网络一样，与普通的深层神经网络形成了鲜明的对比。

- **Demo**
> 在pytorch上实现了多个Highway Networks，其中包括单纯的Highway Networks，以及convolution Highway Networks、LSTm Highway Networks以及Highway Networks的一些变种。
> 
> [Highway Networks implement in pytorch](https://github.com/bamtercelboo/pytorch_Highway_Networks) 


## References ##
- [Highway Networks(paper)](https://arxiv.org/pdf/1505.00387.pdf)

- [Training Very Deep Networks](https://arxiv.org/pdf/1507.06228.pdf)

- [Training Very Deep Networks--Highway Networks ](http://blog.csdn.net/cv_family_z/article/details/50349436)

- [Very Deep Learning with Highway Networks](http://people.idsia.ch/~rupesh/very_deep_learning/)

- [Hightway Networks学习笔记 ](http://blog.csdn.net/sinat_35218236/article/details/73826203?utm_source=itdadao&utm_medium=referral)


## Notation ##
**欢迎转载、转载请注明出处。**



