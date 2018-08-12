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
*这是一篇2016年发表在`NAACL-HLT(Annual Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies)`会议上的论文，作者来自于中国科学技术大学 --- Jian Xu。*

## Abstract ##
`这篇论文的做法比较奇特，而且中间步骤很多`。
已经在前面提到的两篇论文表明中文汉字内部的包含了丰富的语义信息，对中文词向量的表示有着很重要的作用，这篇论文也是基于此来进行相关工作。  
具体来说，是基于前面的`CWE模型`，虽然CWE已经考虑了词的内部组成，增加了语义信息的表示，然而，却忽略了一些问题，在每一个词和他们的组成部分（单字）之间，CWE把单字和词之间的贡献作为一致的，这篇论文提出，他们之间的`贡献度应该是不同的`，CWE忽略了这一问题，本文要利用外部语言来获取语义信息，计算词与单字之间的相似度来表示其贡献的不同，完善相关工作。  
论文提出了联合学习词与字的方法，该方法可以消除中文单字的歧义性，也可以区别出词内部无意义的组成，实验结果表明在 `Word Similarity` 和 `Text Classification` 上验证了其有效性。

## Methodology and Model ##
论文提出的方法可以分为以下几个阶段，`Obtain translations of Chinese words and characters`，`Perform Chinese character sense disambiguation`，`Learn word and character embeddings with our model`。  

### Obtain translations of Chinese words and characters ###
对中文训练语料使用分词工具进行分词，分词工具可以采用jieba，Zpar，thulac，对分词之后的数据进行词性标注（`Part-of-Speech tagging`），词性标注的目的是识别出所有的实体（这里的实体，应该是词性），因为实体词是没有语义信息的，这些词被定义为`non-compositional word`，也就是词的内部组成是没有意义的。    
这里使用了字频来做了下面的一个筛选，提出计算不同词内部单字出现的数量，我称之为字频，字频较低的那些词被认定为是`single-morpheme multi-character words` （像徘徊，琵琶這样的词语，其中的单字很难在其他的词语中使用），定义为 `non-compositional word`。  
下一步的工作让人意想不到，`把中文词语翻译成了英文`，但是这里面并不包含无意义的词（non-compositional word），翻译成英文是为了下面的工作 --- `Perform Chinese character sense disambiguation`。


### Perform Chinese character sense disambiguation ###
这里的工作主要是对中文一字多义的单字消除歧义性，对上文得到的英文语料，通过`CBOW`模型对这份语料进行训练，得到一份英文词向量，对其中区别不是很大的字符进行合并。  
在中文中，相同的词和字符，虽然被应用为不同的词性，但是想要表达的语义信息是一样的。因此，这些被合并为一个，共用一个语义表示。如下图，多个`乐`字可能仅仅在不同的词性之间有所不同，然而语义信息几乎相同。  
![](https://i.imgur.com/N1dNNuS.jpg)  

通过计算相似度来消除歧义，具体的公式如下，  其中c_i，c_j代表的是某个词中的第几个字，Trans(c_i)表示这个字的英文，stop-words(en)代表英文的停用词，x是Trans中的英文，具体来说，看上图，对于`音乐`这个词，c_1表示`音`，c_2表示`乐`，Trans(c_2)表示的是乐在上图中的英文集合，x_3就是pleasure或者是enjoyment。    
![](https://i.imgur.com/d5h5kBc.jpg)  

根据上图的公式就可以计算出字之间的相似度，如果这个值超过了某一个阈值，合并为同一个语义表示。对此，还进行了简化，都是针对一个词被翻译成多个英文的处理，其中一个是把字英文集合取平均值然后计算similarity，另外一个是在所有的候选英文词对中选择相似度值最大的，根据实验表明，后一种方案效果更佳。根据相似度，就可以把简单的解决一下字的歧义性。    
如果max(Sim(x_t, c_k)) > w, c_k是x_t中的第几个字，这样x_t就被定义为 `compositional word`，对于 compositional word 定义如下图，对于`音乐`这个词来说，就被定义为(“音乐”， {Sim(“音乐”, “音”)， Sim(“音乐”, “
乐”)}，{1,1}）。  
![](https://i.imgur.com/169ixoU.jpg)  


### Learn word and character embeddings with our model  --- SCWE ###







## Experiment Result ##






# References  #
[1] Improve Chinese Word Embeddings by Exploiting Internal Structure  
  
 








