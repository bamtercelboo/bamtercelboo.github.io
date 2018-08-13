---
layout:     post
title:      "中文词向量论文综述（三）"
date:       2018-08-14
author:     "bamtercelboo"
header-img: "img/post-bg-2015.jpg"
tags:
    - Word Embedding
    - Paper

---


#  导读  #
最近在做中文词向量相关工作，其中看了一些中文词向量的相关论文，在这篇文章，将把近几年的中文词向量进展及其模型结构加以简述，大概要写3-4篇综述，每篇包含2-3篇论文。续 --- [中文词向量论文综述（二）](https://bamtercelboo.github.io/2018/08/12/chinese_embedding_paper_senond/)。  


# 一、Learning Chinese Word Representations From Glyphs Of Characters #

## 论文来源 ##
*这是一篇2017年发表在`EMNLP(Empirical Methods in Natural Language Processing)`会议上的论文，作者来自于台湾国立大学 --- Tzu-Ray Su 和 Hung-Yi Lee。*


## Abstract ##
这篇论文的出发点也很新颖，中文汉字可以认为是由图形组件组成的，具有丰富的语义信息，基于此，提出了一个新的学习中文词向量的方法，通过图形字符（`character glyphs`）来增强词的表示，character glyphs通过图像卷积从位图（bitmaps）中编码得来，character glyphs特征加强了word的表示，也提高了character embedding。這篇论文虽然是在繁体中文进行的改进，不过idea同样也可以应用在简体中文中。    


## Model ##
這篇论文的模型参考了`CWE模型`和`MGE模型`，模型部分也是分为了几个阶段，第一个阶段是通过convAE从位图中抽取glyph特征，第二阶段是在已有的中文词向量模型中进行改进提高，像CWE，MGW模型，第三阶段是直接使用glyph特征学习中文词向量表示。  

### Character Bitmap Feature Extraction ###
前期把字符全部转换成图像，通过convAE对图像抽取特征，convAE的模型结构图如下图所示，通过convAE最后的输出得到的512维的特征，character的glyph特征表示为g_k。    
![](https://i.imgur.com/QjDyXxJ.jpg)


### Glyph-Enhanced Word Embedding (GWE) ###
在這部分对`CWE模型`做了两个调整分别构建了`CWE+ctxG模型`和`CWE+tarG模型`。  
1. **Enhanced by Context Word Glyphs --- CWE+ctxG模型**   
在CWE的基础之上增加了上下文词的glyph特征， 模型图如下所示，  
![](https://i.imgur.com/SeAGnKc.jpg)  
其中，W(ctxG)_i的表示如下，其实计算就是`word embedding + avgall(character embedding + glyph embedding)`，    
![](https://i.imgur.com/Wl0pX28.jpg)


2. **Enhanced by Target Word Glyphs --- CWE+tarG模型**  
CWE+tarG模型和上文差不多，不过这个加入的是目标词的glyph特征，具体的模型图如下。  
![](https://i.imgur.com/AtWHXBW.jpg)  



### Directly Learn From Character Glyph Features ###
在这部分仅仅通过glyph特征与RNN循环神经网络构建了两个模型，分别是 `RNN-Skipgram` 和 `RNN-Glove`。    
1. **RNN-Skipgram**  
RNN-Skipgram是把RNN和skipgram结合，通过RNN对glyph特征进行编码，产生隐层表示，然后把隐层表示作为skipgram的输入，进行预测，具体的模型结构图如下图所示。  
![](https://i.imgur.com/785Vs3o.jpg)  


2. **RNN-Glove**  
通过两个RNN循环神经网络，输入分别是中心词和上下文词的glyph特征，与RNN-Skipgram有微小的差别，输入中心词的网络后连接的是一个共享网络，输入上下文词的网络后面是全连接层，然后两个的输出的内积就是log(X_ij)的预测。

![](https://i.imgur.com/k5qn20q.jpg)



## Experiment Result ##


















# 二、 #

## 论文来源 ##



## Abstract ##


## Model ##


## Experiment Result ##






# References  #
[1]   

  
 








