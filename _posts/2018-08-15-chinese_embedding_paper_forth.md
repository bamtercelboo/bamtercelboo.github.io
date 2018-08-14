---
layout:     post
title:      "中文词向量论文综述（四）"
date:       2018-08-15
author:     "bamtercelboo"
header-img: "img/post-bg-2015.jpg"
tags:
    - Word Embedding
    - Paper

---


#  导读  #
最近在做中文词向量相关工作，其中看了一些中文词向量的相关论文，在这篇文章，将把近几年的中文词向量进展及其模型结构加以简述，大概要写3-4篇综述，每篇包含2-3篇论文。续 --- [中文词向量论文综述（三）](https://bamtercelboo.github.io/2018/08/14/chinese_embedding_paper_thrid/)。  


# 一、Enriching Word Vectors with Subword Information #

## 论文来源 ##
*这是一篇2017年发表在`ACL(Association for Computational Linguistics)`会议上的论文，作者来自于Facebook AI Research --- Piotr Bojanowski ，Edouard Grave 。*


## Abstract ##
这篇论文虽然是针对英文等西方语言提出的想法，但是后面`cw2vec`将这个idea在中文词向量上进行了应用，在这里还是简单的介绍一下。  

在英文中，每一个单词由若干个字母组成，单词的词义和其中的组成是有很大的关系的，这篇论文的核心思想就是采用单词的`n-gram特征`学习词向量的表示，并取得了很好的实验效果。  


## Model ##
这篇论文提出的方法也很简单，在每个word的前后分别添加` < 与 > `字符，作为这个单词的开始于结束，还有就是对于只有一个字母的word进行表示，然后抽取其`n-gram词袋特征`，具体来说，以`3-gram`为例，单词`where`，可以被表示成`<wh，whe，her，ere，re>`，单词`a`，可以表示为`<a>`，这篇论文抽取的是`3 至 6的n-gram`，那么where的所有表示就是，`3-ngram：<wh，whe，her，ere，re>，<whe`，`4-gram：<whe，wher，here，ere>`，`5-gram：<wher，where，here>`，`6-gram：<where，where>`，以上就是where的所有表示，除此之外，还把原单词`<where>`加入到n-gram中，`最后word采用的是所有的n-gram的和。`     


这篇论文没有提供模型结构图，但是都是基于CBOW和skipgram进行的改善。  


## Experiment Result ##
这篇论文的实验部分，在`Human similarity judgement` 和 `Word analogy tasks`上面做了比较，`而且是在多种语言进行了实验`，具体的实验结果如下图所示，其中`sg`代表skipram，`sisg-`代表的是对那些不在评测文件中出现的词采用不做处理，`sisg`代表的是不在评测文件中的词采用n-gram加和表示。  
1. **Human similarity judgement**  
![](https://i.imgur.com/P3Mvlok.png)

2. **Word analogy tasks**    
![](https://i.imgur.com/zQmpjjq.png)




# 二、 cw2vec: Learning Chinese Word Embeddings with Stroke n-gram Information #

## 论文来源 ##
*这是一篇2018年发表在`AAAI 2018(Association for the Advancement of Artificial Intelligence 2018)`会议上的论文，作者来自于蚂蚁金服人工智能部 --- 曹绍升  。*

## 详解 ##
这篇我在前面已经对其理论进行了总结，并且实现了一个C++版本，具体的可以查看，[cw2vec理论及其实现](https://bamtercelboo.github.io/2018/05/11/cw2vec/)。  

  
# 三、Radical Enhanced Chinese Word Embedding #

## 论文来源 ##
*这是一篇2018年发表在`CCL2018(The Seventeenth China National Conference on Computational Linguistics, CCL 2018)`会议上的论文，作者来自于电子科技大学 --- Zheng Chen 和 Keqi Hu 。*


## Abstract ##



## Model ##



## Experiment Result ##



# References  #
[1] Enriching Word Vectors with Subword Information  
[2] cw2vec: Learning Chinese Word Embeddings with Stroke n-gram Information  

  



  
 








