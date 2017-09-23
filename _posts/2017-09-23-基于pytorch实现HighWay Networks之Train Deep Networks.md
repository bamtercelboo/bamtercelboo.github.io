---
layout:     post
title:      "基于pytorch实现Highway Networks之Train Deep Networks"
date:       2017-09-23
author:     "bamtercelboo"
header-img: "img/post-bg-2015.jpg"
tags:
    - 博客园
---


## （一）Highway Networks 与 Deep Networks 的关系##


> 1. 理论实践表明神经网络的深度是至关重要的，深层神经网络在很多方面都已经取得了很好的效果，例如，在1000-class ImageNet数据集上的图像分类任务通过利用深层神经网络把准确率从84%提高到了95%，然而，在训练深层神经网络的时候却是非常困难的，神经网络的层数越多，存在的问题也就越多（例如大家熟知的梯度消失、梯度爆炸问题，下文会详细讲解）、训练起来也就是愈加困难，这是一个公认的难题。


> 2. 2015年由Rupesh Kumar Srivastava等人提出的新的网络结构（Highway Networks）很好的解决了这一个问题，**Highway Networks 允许信息“高速无阻碍”的通过各个神经层**，这就不会出现深层网络中出现的信息阻碍的问题。在此之前，深层神经网络的深度仅仅能够达到几层或者是十几层，但是Highway Networks可以训练数十层甚至上百层的神经网络（前提是硬件设置可以支持这种大量的运算）。


## （二）Deep Networks 梯度消失/爆炸（vanishing and exploding gradient）问题##

1、什么是梯度消失/爆炸？
> 在反向传播的过程中，前面层的权重正常学习更新，而接近后面的层权重基本上不更新，导致后面的层基本上学习不到任何的东西，也就是说后面的层只是相当于对输入做了一个映射，那么这样的深层神经网络也就仅仅相当于浅层的神经网络了。

2、梯度消失/爆炸
> 我们先来看一下简单的深层神经网络（仅仅几个隐藏层）
> 
> ![](https://i.imgur.com/eg3bMXJ.png)
> 
> 先把各个层的公式写出来

> C=sigmoid(W_4*H_3  +b_4)
> 
> H_3=sigmoid(W_3*H_2  +b_3)
> 
> H_2=sigmoid(W_2*H_1  +b_2)
> 
> H_1=sigmoid(W_1*x +b_1)
> 
> 对W_1求导
> 
> ![](https://i.imgur.com/yYlxgbB.gif)
> 
> W=W - lr * g(t)
> 
> 以上公式仅仅是四个隐藏层的情况，当隐藏层的数量达到数十层甚至是数百层的情况下，一个一个的反向传播回去，当权值 < 1的时候，传到最后一层近乎0，例如，〖0.9〗^100已经是很小很小了，这就造成了只有前面几层能够正常的反向传播，后面的那些隐藏层仅仅相当于输入x的权重的映射，权重不进行更新。反过来，当权值 > 1的时候，会造成梯度爆炸，同样是仅仅前面的几层能更改正常学习，后面的隐藏层会变得很大很大。


## References ##
- [Highway Networks(paper)](https://arxiv.org/pdf/1505.00387.pdf)

- [为什么深层神经网络难以训练](http://blog.csdn.net/binchasing/article/details/50300069)

- [Why are deep neural networks hard to train?](http://neuralnetworksanddeeplearning.com/chap5.html)

- [Neural Networks and Deep Learning学习笔记ch5 - 为什么深度神经网络很难训练? ](http://blog.csdn.net/yc461515457/article/details/50571559)

## Notation ##
**欢迎转载、转载请注明出处。**






