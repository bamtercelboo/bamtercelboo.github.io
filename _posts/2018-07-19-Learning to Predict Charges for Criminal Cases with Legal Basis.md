---
layout:     post
title:      "Learning to Predict Charges for Criminal Cases with Legal Basis"
date:       2018-07-19
author:     "bamtercelboo"
header-img: "img/post-bg-2015.jpg"
tags:
    - LJP
    - Paper

---


#  导读  #
2017年EMNLP(Conference on Empirical Methods in Natural Language)收录了论文《Learning to Predict Charges for Criminal Cases with Legal Basis》，作者是北京大学---罗炳峰。最近看了这篇论文，对其做一个简单的概述。


#  背景知识  #
近些年来，Legal Jugement Prediction 任务越来越引起大家的关注，这个任务的目的是通过给定的事实描述，预测出罪名，法条以及刑期等相关信息，charge prediction 任务就是这样的一个任务，这对一些法律助手是很有帮助的，对法官判决也有很大的帮助，不仅如此，对那些法律知识知之甚少的人也会有一定的积极作用。  
目前，这类任务的主流做法是基于文本分类的框架，像流行的SVM，CNN，LSTM等这些深度学习框架，然而，作者认为，仅仅通过给定的事实描述来做，不能够很好的解决问题，他认为，法条信息在这个任务上有很重要的作用，所以，作者通过加入法条特征，使用attention机制，提出了这个任务新的方法，通过他的实验结果也确实表明法条起着至关重要的作用。

#  数据处理  #
数据来源于中国裁判文书网，收集了50000个文本用作训练，5000个文本用于开发，5000个文本用于测试，50000个训练文本中，把罪名的频度低于80的看做消极数据，不作处理，仅仅处理频度高于80的数据，数据的格式如下图。
      
对于法条部分，考虑刑事法律，结果数据集中包含50个不同的罪名，321条不同的相关法条，每个事实描述平均383个词，根据下图，高亮的部分，能够很容易通过正则表达式抽取相关特征。  
  
由于目前很难匹配多个罪名，所以这篇论文仅仅考虑了一个罪名的情况，并没有做多个罪名的情况。


![](https://i.imgur.com/CyiKJvu.png)


# References  #
[1] Learning to Predict Charges for Criminal Cases with Legal Basis
 








