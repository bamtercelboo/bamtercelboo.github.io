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
2017年EMNLP(Conference on Empirical Methods in Natural Language)收录了论文《Learning to Predict Charges for Criminal Cases with Legal Basis》，作者是北京大学---罗炳峰。最近看了这篇论文，对其做一个简单的概述，时间有限，没有做代码复现。


#  背景知识  #
近些年来，Legal Jugement Prediction 任务越来越引起大家的关注，这个任务的目的是通过给定的事实描述，预测出罪名，法条以及刑期等相关信息，charge prediction 任务就是这样的一个任务，这对一些法律助手是很有帮助的，对法官判决也有很大的帮助，不仅如此，对那些法律知识知之甚少的人也会有一定的积极作用。  
目前，这类任务的主流做法是基于文本分类的框架，像流行的SVM，CNN，LSTM等这些深度学习框架，然而，作者认为，仅仅通过给定的事实描述来做，不能够很好的解决问题，他认为，法条信息在这个任务上有很重要的作用，所以，作者通过加入法条特征，使用attention机制，提出了这个任务新的方法，通过他的实验结果也确实表明法条起着至关重要的作用。




# References  #
[1] Learning to Predict Charges for Criminal Cases with Legal Basis
 








