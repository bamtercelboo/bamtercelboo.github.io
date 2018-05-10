---
layout:     post
title:      "中文维基百科数据处理"
date:       2018-05-10
author:     "bamtercelboo"
header-img: "img/post-bg-2015.jpg"
tags:
    - wikipedia

---


# 导读  #

- 最近在做词向量相关工作，词向量的训练数据采用中文维基百科数据，训练之前，要对维基百科数据进行处理，这篇文章记录了一些处理过程及相关的脚本。

# 一 、维基百科  #

-  维基百科（Wikipedia），是一个基于维基技术的多语言百科全书协作计划，也是一部用不同语言写成的网络百科全书。维基百科是由吉米·威尔士与拉里·桑格两人合作创建的，于2001年1月13日在互联网上推出网站服务，并在2001年1月15日正式展开网络百科全书的项目。

# 二 、维基百科处理  #

## 1、环境配置 ##

- （1）、编程语言采用 python3
- （2）、Gensim第三方库，Gensim是一个Python的工具包，其中有包含了中文维基百科数据处理的类，使用方便。
	- Gensim : [https://github.com/RaRe-Technologies/gensim](https://github.com/RaRe-Technologies/gensim)
	- 使用 `pip install gensim` 安装gensim。

- （3）、OpenCC第三方库，是中文字符转换，包换中文简体繁体相互转换等。
	- OpenCC：[https://github.com/BYVoid/OpenCC](https://github.com/BYVoid/OpenCC)，OpenCC源码采用c++实现，如果会用c++的可以使用根据介绍，make编译源码。
	- OpenCC也有python版本实现，可以通过pip安装（`pip install opencc-python`），速度要比c++版慢，但是使用方便，安装简单，推荐使用pip安装。


## 2、数据下载 ##

- 中文维基百科数据按月进行更新备份，一般情况下，下载当前最新的数据，[下载地址（https://dumps.wikimedia.org/zhwiki/latest/）](https://dumps.wikimedia.org/zhwiki/latest/)，我们下载的数据是：zhwiki-latest-pages-articles.xml.bz2。

- 中文维基百科数据一般包含如下几个部分：
- ![](https://i.imgur.com/KsLfRqK.jpg)

- 训练词向量采用的数据是正文数据，下面我们将对正文数据进行处理。


## 3、数据抽取 ##

- 下载下来的数据是压缩文件（bz2，gz），不需要解压，这里已经写好了一份利用gensim处理维基百科数据的脚本（[wikidata_process](https://github.com/bamtercelboo/corpus_process_script/tree/master/wikidata_process)）

- 使用：
#  
	python wiki_process.py zhwiki-latest-pages-articles.xml.bz2 zhwiki-latest.txt

- 这部分需要一些的时间，处理过后的得到一份中文维基百科正文数据（zhwiki-latest.txt）。

- 输出文件类似于：  
#  
	歐幾里得 西元前三世紀的古希臘數學家 現在被認為是幾何之父 此畫為拉斐爾的作品 雅典學院 数学 是利用符号语言研究數量 结构 变化以及空间等概念的一門学科

## 4、中文繁体转简体 ##

- 经过上述脚本得到的文件包含了大量的中文繁体字，我们需要将其转换成中文简体字。

- 我们利用OpenCC进行繁体转简体的操作，这里已经写好了一份python版本的脚本来进行处理（[chinese_t2s](https://github.com/bamtercelboo/corpus_process_script/tree/master/chinese_t2s)）

- 使用：
#
	python chinese_t2s.py --input input_file --output output_file
	like:
	python chinese_t2s.py --input zhwiki-latest.txt --output zhwiki-latest-simplified.txt

- 输出文件类似于
#
	欧几里得 西元前三世纪的古希腊数学家 现在被认为是几何之父 此画为拉斐尔的作品 雅典学院 数学 是利用符号语言研究数量 结构 变化以及空间等概念的一门学科

## 5、清洗语料 ##

- 上述处理已经得到了我们想要的数据，但是在其他的一些任务中，还需要对这份数据进行简单的处理，像词向量任务，在这得到的数据里，还包含很多的英文，日文，德语，中文标点，乱码等一些字符，我们要把这些字符清洗掉，只留下中文字符，仅仅留下中文字符只是一种处理方案，不同的任务需要不同的处理，这里已经写好了一份脚本（[clean](https://github.com/bamtercelboo/corpus_process_script/tree/master/clean)）。

- 使用：
#
	python clean_corpus.py --input input_file --output output_file
	like：
	python clean_corpus.py --input zhwiki-latest-simplified.txt --output zhwiki-latest-simplified_cleaned.txt

- 效果：
#
	input:
	哲学	哲学（英语：philosophy）是对普遍的和基本的问题的研究，这些问题通常和存在、知识、价值、理性、心灵、语言等有关。
	output:
	哲学哲学英语是对普遍的和基本的问题的研究这些问题通常和存在知识价值理性心灵语言等有关

# 三 、数据处理脚本  #

- 最近在github上新开了一个Repository([corpus-process-script](https://github.com/bamtercelboo/corpus_process_script))，在这个repo，将存放中英文数据处理脚本，语言不限，会有详细的README，希望对大家能有一些帮助。

## References  ##

[1] [繁体转简体，CentOS安装OpenCC，升级到gcc4.6](http://www.linuxdown.net/install/soft/2016/0122/4445.html)  
[2] [OpenCC - 简体繁体转换](https://www.jianshu.com/p/834a02d085b6)  
[3] [wiki语料处理](http://www.cnblogs.com/chenbjin/p/5635853.html)  
[4] [中英文维基百科语料上的Word2Vec实验](http://www.52nlp.cn/%E4%B8%AD%E8%8B%B1%E6%96%87%E7%BB%B4%E5%9F%BA%E7%99%BE%E7%A7%91%E8%AF%AD%E6%96%99%E4%B8%8A%E7%9A%84word2vec%E5%AE%9E%E9%AA%8C)

