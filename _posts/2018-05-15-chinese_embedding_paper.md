---
layout:     post
title:      "中文词向量论文综述"
date:       2018-08-10
author:     "bamtercelboo"
header-img: "img/post-bg-2015.jpg"
tags:
    - Word Embedding
    - Paper

---


#  导读  #
最近在做中文词向量相关工作，其中看了一些中文词向量的相关论文，在这篇文章，将把近几年的中文词向量进展及其模型结构加以简述。


# 一、Component-Enhanced Chinese Character Embeddings #

## 论文来源 ##
这是一篇发表在2015年EMNLP会议上的论文，作者来自于香港理工大学 --- 李嫣然。

## Abstract ##
在目前的NLP各项任务中，词向量已经得到了广泛的应用并取得了很好的效果，然而大多数是对于英文等西方语言，对于中文，由于中文汉字包含了巨大的信息，在中文词向量的工作中有很大的提升，这篇论文认为汉字的组件（部首）包含了大量的语义信息，基于此提出了两个词向量模型，对中文字向量进行了改善，实验结果表明在文本分类已经词相似度上都得到了提升。

## Model ##
模型结构图如下，具体做法是抽取每个汉字的组件组成一个component列表（可以从在线新华词典获取component列表），部首信息要比其他的组件信息包含更加丰富的语义信息，所以，把部首放在了component列表的首位进行训练，下图中的E代表的就是component列表，C代表的是上下文词， Z代表的是目标词。  
![](https://i.imgur.com/46CRvTY.jpg)  ![](https://i.imgur.com/TshmPrx.jpg)

具体做法，以charCBOW为例，charCBOW是在原始的CBOW的基础之上进行的改善，把E和C进行cat连接作为特征。    

也提供了一些部首信息，如下图。  
![](https://i.imgur.com/KmB32WF.jpg)

## Experiment Result ##
在Word Similarity 和 Text Classification 上面进行了实验。  
Word Similarity采用的评估文件大多数都是基于英文构建的，像 WS-353，RG-65等，对于中文来说，仅有HowNet和 E-TC（哈工大词林），由于HowNet包含较少的现代词，选择采用E-TC进行评测；Text Classification  选择的数据集是腾讯新闻（Tencent news datasets），在Word Similarity 和 Text Classification上面都验证了论点。下图是实验结果。
![](https://i.imgur.com/99pznZG.jpg)



# 二、 #





#  进度  #
目前较忙，会尽快总结完成。开始抽时间整理。


# References  #
[1] Component-Enhanced Chinese Character Embeddings
 








