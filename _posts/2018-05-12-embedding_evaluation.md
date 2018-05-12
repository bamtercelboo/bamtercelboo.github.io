---
layout:     post
title:      "中英文词向量评测"
date:       2018-05-12
author:     "bamtercelboo"
header-img: "img/post-bg-2015.jpg"
tags:
    - Word Embedding

---


#  导读  #
最近在做词向量相关工作，训练的词向量如何进行评测？本文将从业界使用最广泛的两个评测任务进行阐述，包括相似度任务（word similarity task）和词汇类比任务(word analogy task)，这里已经写好了相关评测脚本（[Word_Similarity_and_Word_Analogy](https://github.com/bamtercelboo/Word_Similarity_and_Word_Analogy)），包括中文词向量评测脚本和英文V词向量评测脚本，方便大家使用。

#  相关知识 #
对于词向量好坏的评测，业界最常用的也是最快的评测方式是计算词之间的相似度任务（word similarity task）和与之相关的是词汇类比任务（word analogy task），然而，近两年来，词向量仅仅在这两个任务上进行评测已经不在得到公认，要想得到公认，词向量的好坏需要应用到具体任务中进行评测，包括句子分类，文本分类，词性标注(Part-of-Speech tagging)，命名实体识别（NER）等，但是这两个任务还是最基本的评测，词向量的相关论文中也会进行这部分的实验。





# References  #
[1] [Word2vec Demo](http://www.wordvectors.org/)   
[2] Faruqui, Manaal, and Chris Dyer. "Community evaluation and exchange of word vectors at wordvectors. org." Proceedings of 52nd Annual Meeting of the Association for Computational Linguistics: System Demonstrations. 2014.
[3] 







