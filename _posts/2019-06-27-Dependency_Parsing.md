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
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;依存句法理论中依存是指词与词之间支配与被支配的关系，这种关系不是对等的，这种关系具有方向指向。确切的说，处于支配地位的成分称之为`支配者(governor,regent,head)`，而处于被支配地位的成分称之为`从属者(modifier,subordinate,dependency)`。依存关系连接的两个词分别是`核心词(head)`和`依存词(dependent)`。依存关系可以细分为不同的类型，表示两个词之间的具体句法关系。

#  三、Deep Biaffine Attention for Neural Dependency Parsing  #



#  四、实验设置及实验结果  #
## 4.1 数据 ##
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
## 4.2 实验结果 ##
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp

## 4.3 代码开源 ##

#  五、总结  #



# References  #
[1]  [Deep Biaffine Attention for Neural Dependency Parsing](https://arxiv.org/abs/1611.01734)  
[2] https://zhuanlan.zhihu.com/p/51186364  








  



  
 








