---
layout:     post
title:      "中文词向量论文综述（二）"
date:       2018-08-12
author:     "bamtercelboo"
header-img: "img/post-bg-2015.jpg"
tags:
    - Word Embedding
    - Paper

---


#  导读  #
最近在做中文词向量相关工作，其中看了一些中文词向量的相关论文，在这篇文章，将把近几年的中文词向量进展及其模型结构加以简述，大概要写3-4篇综述，每篇包含2-3篇论文。续 --- [中文词向量论文综述（一）](https://bamtercelboo.github.io/2018/08/10/chinese_embedding_paper_first/)。  


# 一、Improve Chinese Word Embeddings by Exploiting Internal Structure #

## 论文来源 ##
*这是一篇2016年发表在`NAACL-HLT(Annual Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies)`会议上的论文，作者来自于中国科学技术大学 --- Jian xu。*

## Abstract ##
已经在前面提到的两篇论文表明中文汉字内部的包含了丰富的语义信息，对中文词向量的表示有着很重要的作用，这篇论文也是基于此来进行相关工作。  
具体来说，是基于前面的`CWE模型`，虽然CWE已经考虑了词的内部组成，增加了语义信息的表示，然而，却忽略了一些问题，在每一个词和他们的组成部分（单字）之间，CWE把单字和词之间的贡献作为一致的，这篇论文提出，他们之间的`贡献度应该是不同的`，CWE忽略了这一问题，本文要利用外部语言来获取语义信息，计算词与单字之间的相似度来表示其贡献的不同，完善相关工作。  
论文提出了联合学习词与字的方法，该方法可以消除中文单字的歧义性，也可以区别出词内部无意义的组成，实验结果表明在 `Word Similarity` 和 `Text Classification` 上验证了其有效性。

## Model ##




## Experiment Result ##






# References  #
[1] Improve Chinese Word Embeddings by Exploiting Internal Structure  
  
 








