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

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如下图列举出一个依存句法分析的例子:  
![](https://i.imgur.com/ZPkhN25.jpg)  


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `Dependency Parsing` 主要有两种方法：[Transition-based](https://zhuanlan.zhihu.com/p/59619401) 和 `Graph-based`。  


#  三、Deep Biaffine Attention for Neural Dependency Parsing  #

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;基于图的依存句法分析从左向右解析句子，针对句中的每个词，找该词的head词(该词到head词之间的arc)以及从该词到head词之间的依存关系类型,即需要解决两个问题：哪两个节点连依存弧以及弧的标签是什么。目前的深度学习的方法使用分类器来解决这两个问题。该模型是针对图的依存句法分析，是对Kiperwasser & Goldberg(2016),Hashimoto et al.(2016), and Cheng et al.(2016)提出的模型加以修改。主要的修改如下：  
- 使用双仿射注意力机制(Biaffine Attention)代替双线性(bilinear)或传统的MLP-based注意力机制, 运用了一个双线性层而不是两个线性层和一个非线性层。  
- 使用Biaffine依存标签分类器。  
- 在双仿射变换(Biaffine transformation)之前，将降维MLP应用于每个循环输出。  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;biaffine并不是双线性(bilinear)或MLP机制，它使用一个仿射变换在单个LSTM输出状态r预测所有类别上的得分。在本文提出的双仿射注意力机制(Biaffine Attention)可以看做为一个传统的仿射分类器(公式1)，但是对stacked LSTM的输出RU(1)进行一个 (d×d)线性变换代替权重矩阵W，并且对Ru(2)采用一个(d×1)线性变换来替代偏置项b(公式2)。  

![](https://i.imgur.com/L5Vim2W.jpg)    


## arc得分 ##
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;若句子中有N个单词，包含虚根ROOT在内一共d=N+1个词。对每个词都需要得到一个分数si。因为句子中的词的个数是不确定的，所以这是一个不定类别分类问题。而一般MLP是个固定类别的分类器(公式1)，为了能够处理不定类别分类问题，本文采用两个MLP对BILSTM隐层输出向量进行重新编码(公式4、公式5)。  然后套用公式(2)得到公式(6), 得到分数。这里两个MLP分别针对于dep和head。MLP得到的向量表示通常更小，好处是能够去除多余的信息。因为原始BiLSTM隐层中含有预测依存弧标签的信息。对预测head无用。   

![](https://i.imgur.com/csQesyS.jpg)  


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本文把上述公式称之为deep bilinear attention mechanism，因为并没有直接用RNN输出的向量表示，而是采用了对head和dep专用的两个MLP进行再次编码。这里并没有用到熟悉的attention公式，但是称之为attention的原因是，输入是所有时刻的LSTM隐层向量表示，输出是一个在各个时刻上归一化之后向量表示。和其它Graph-based模型一样，在训练时，预测的解析树是每一个单词都依存于其得分最高的head(虽然在测试时也会通过MST算法确保解析树是一个格式良好的树)。  


## arc标签 ##
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;head与dep之间的依存关系数目是确定的，这是一个确定类别的分类问题,采用下述公式(3)计算标签分数。  

![](https://i.imgur.com/8Lq1wfe.jpg)    

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  这里的优势在于可以直接对单词 j 在第二项收到任何dependents的先验概率和 j 在第一项中收到特定依存项 i 的可能性之间进行建模。还双仿射分类器来预测给定的head或预测对应的依存标签。假设一共有m个标签，U(1)是m x d x d的高阶tensor，ri是第i个词在BiLSTM的输出向量表示(d x 1)，yi是第i个词head，ryi对应的是其BiLSTM的向量表示(d x 1)。 
 
## 整体结构图 ##
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;模型的整体结构图：  ![](https://i.imgur.com/W9gEgzX.jpg)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;该模型图从下向上看，输入是词与词性向量拼接之后的向量表示，通过BiLSTM提取到特征ri，经过两个不同的MLP分别得到 h(arc−dep) 和 h(arc−head) ，d(所有词)个这样的h stack得到H(arc−dep)和H(arc−head)，并且H(arc−dep)额外拼接了一个单位向量。利用中间矩阵U(arc)进行仿射变换，每个词以dep的身份与以head的身份的每个词进行点积，得到arc成立的分数矩阵S(arc)。也就是上述公式(6)得到的结果。

#  四、实验设置及实验结果  #
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Github.  [bamtercelboo/PyTorch_Biaffine_Dependency_Parsing](https://github.com/bamtercelboo/PyTorch_Biaffine_Dependency_Parsing)  


#  五、总结  #
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本文是对Deep Biaffine Attention for Neural Dependency Parsing做的一个简单的总结，同时也是NLPCC2019 shared tasks(跨领域依存句法分析)的一个baseline方法。

# References  #
[1]  [Deep Biaffine Attention for Neural Dependency Parsing](https://arxiv.org/abs/1611.01734)  
[2] https://zhuanlan.zhihu.com/p/51186364  
[3] https://xiaoxiaoaurora.github.io/2019/04/11/Deep-Biaffine-Attention-for-Neural-Dependency-Parsing/  
[4] http://www.hankcs.com/nlp/parsing/deep-biaffine-attention-for-neural-dependency-parsing.html  
[5] http://hlt.suda.edu.cn/index.php/Nlpcc-2019-shared-task









  



  
 








