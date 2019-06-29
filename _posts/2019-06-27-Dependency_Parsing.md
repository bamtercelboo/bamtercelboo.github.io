---
layout:     post
title:      "Deep Biaffine Attention for Neural Dependency Parsing"
date:       2019-06-27
author:     "bamtercelboo"
header-img: "img/post-bg-2015.jpg"
tags:
    - Denpendency Parsing
    - Biaffine

---


#  一、导读  #
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`句法分析(syntactic parsing)`是NLP中的关键技术之一，通过对输入的文本句子进行分析获取其句法结构。句法分析通常包括三种：  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(1) `句法结构分析(syntactic structure parsing)`，又称`短语结构分析(phrase structure parsing)`、`成分句法分析(constituent syntactic parsing)`。作用是识别出句子中的短语结构以及短语之间的层次句法关系。  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(2)`依存关系分析`，又称`依存句法分析（dependency syntactic parsing），简称依存分析(denpendency parsing)`，作用是识别句子中词与词之间的相互依存关系。  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(3`)深层文法句法分析`，即利用深层文法，例如词汇化树邻接文法(Lexicalized Tree Adjoining Grammar, LTAG)、词汇功能文法(Lexical Functional Grammar,LFG)、组合范畴文法(Combinatory Categorial Grammar,CCG)等, 对句子进行深层的句法以及语义分析。

#  二、依存分析  #
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`百度百科定义`：依存句法是由法国语言学家L.Tesniere最先提出。它将句子分析成一颗依存句法树，描述出各个词语之间的依存关系。  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;依存句法理论中依存是指词与词之间支配与被支配的关系，这种关系不是对等的，这种关系具有方向指向。确切的说，处于支配地位的成分称之为`支配者(governor,regent,head)`，而处于被支配地位的成分称之为`从属者(modifier,subordinate,dependency)`。依存关系连接的两个词分别是`核心词(head)`和`依存词(dependent)`。依存关系可以细分为不同的类型，表示两个词之间的具体句法关系, 依存关系用一个有向弧表示，叫做依存弧。依存弧的方向为由从属词指向支配词。  

如下图列举出一个依存句法分析的例子:  
![](https://i.imgur.com/ZPkhN25.jpg)  


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `Dependency Parsing` 主要有两种方法：[Transition-based](https://zhuanlan.zhihu.com/p/59619401) 和 `Graph-based`。  


#  三、Deep Biaffine Attention for Neural Dependency Parsing  #
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;模型的整体结构图：  ![](https://i.imgur.com/W9gEgzX.jpg)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;基于图的依存句法分析从左向右解析句子，针对句中的每个词，找该词的head词(该词到head词之间的arc)以及从该词到head词之间的依存关系类型,即需要解决两个问题：哪两个节点连依存弧以及弧的标签是什么。目前的深度学习的方法使用分类器来解决这两个问题。该模型是针对图的依存句法分析，是对Kiperwasser & Goldberg(2016),Hashimoto et al.(2016), and Cheng et al.(2016)提出的模型加以修改。主要的修改如下：  
- 使用双仿射注意力机制(Biaffine Attention)代替双线性(bilinear)或传统的MLP-based注意力机制, 运用了一个双线性层而不是两个线性层和一个非线性层。  
- 使用Biaffine依存标签分类器。  
- 在双仿射变换(Biaffine transformation)之前，将降维MLP应用于每个循环输出。  

biaffine的选择而不是双线性或延时机制使得分类器在我们的模型中类似传统的仿射分类器,它使用一个仿射变换在单个LSTM输出状态r(或其他向量输入)预测矢量的分数我所有类(1)
 
## arc得分 ##
若句子中有N个单词，包含虚根ROOT在内一共d=N+1个词。对每个词都需要得到一个分数si。因为句子中的词的个数是不确定的，所以这是一个不定类别的分类问题。可将双仿射注意力机制看作一个传统的放射分类器，但是使用堆叠LSTM的输出RU(1)的一个 (d×d)线性变换代替权重矩阵W，用一个(d×1)变换Ru(2)来替代偏置项b

而一般MLP是个固定类别的分类器（公式1）,为了能够处理不确定类别分类问题，本文采用两个MLP对BILSTM隐层输出向量进行重新编码(公式4、公式5)。   
![](https://i.imgur.com/DdMhRgm.jpg)  

这里两个MLP分别针对于dep和head。MLP得到的向量表示通常更小，好处是能够去除多余的信息。因为原始BiLSTM隐层中含有预测依存弧标签的信息。对预测head无用。  



#  四、实验设置及实验结果  #
## 4.1 数据 ##
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
## 4.2 实验结果 ##
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

## 4.3 代码开源 ##

#  五、总结  #



# References  #
[1]  [Deep Biaffine Attention for Neural Dependency Parsing](https://arxiv.org/abs/1611.01734)  
[2] https://zhuanlan.zhihu.com/p/51186364  
[3] https://xiaoxiaoaurora.github.io/2019/04/11/Deep-Biaffine-Attention-for-Neural-Dependency-Parsing/  








  



  
 








