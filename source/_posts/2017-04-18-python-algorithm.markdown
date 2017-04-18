---
layout: post
title: "Python_algorithm"
date: 2017-04-18 13:21:33 +0800
comments: true
categories: 
---
# Python 常用的机器学习算法库介绍
------
Python作为目前最火的学习机器学习算法的语言之一拥有如下三个优点：

>1. 语法简单，上手容易
>2. 功能多样
>3. 强大的社区
>4. 丰富的机器学习库


##[Scikit-learn](http://scikit-learn.org/stable/)
GitHub: https://github.com/scikit-learn/scikit-learn

Scikit-learn是建立在Scipy和Numpy基础上的机器学习库。包含丰富的分类，回归，聚类，降维，模型选择以及预处理的方法。
>注：NumPy 是以矩阵为基础的数学计算模块，Scipy是科学计算函数库。NumPy主要是纯数学的函数，Scipy包含一些高阶的抽象模型。

![](/Users/chenlini/octopress/pic/Scikit-learn.png)

######其中非监督的学习算法包括：岭回归，lasso回归，Elastic Net，逻辑回归，核函回归，SVM，朴素贝叶斯，决策树，增强算法等。

######非监督学习算法有K-Means，Affinity propagation，Mean-shift，Spectral clustering，Ward hierarchical clustering（层次聚类），Agglomerative clustering（密度聚类），DBSCAN，Gaussian mixtures。



##[Theano](http://deeplearning.net/software/theano/)

Github: https://github.com/Theano/Theano

Theano允许你定义、优化和评估涉及多维数组的数学表达式。能够很好的支持NumPy，有完善的文档以及教程，如下图所示。该库比较偏向学术研究，方向为神经网络与深度学习的领域。

![](/Users/chenlini/octopress/pic/Theano.png)

>* [Pylearn2](http://deeplearning.net/software/pylearn2/)就是在Theano基础上建立的，把一些较为常用的深度学习的模型以及训练算法封装成了包，可以直接调用。
>* [Keras](https://keras.io/)也是在Theano基础上建立的，是较为流行的，高度模块化的深度学习框架。

##[Tensorflow](http://www.tensorfly.cn/tfdoc/tutorials/overview.html)

Github: https://github.com/tensorflow/tensorflow/issues

Tensorflow是现在最流行的深度学习库，利用数据流图形进行数值计算。被评选为2016年最值得fork的项目之一。该库主要由C++实现，但是有Python的API。最重要的是有中文社区以及中文文档！

主要的研究方向是**神经网络**。
![](/Users/chenlini/octopress/pic/tensorflow.png)

#####其他库：
>* [Pyevolve](http://pyevolve.sourceforge.net/):遗传算法
>* [nupic](http://www.numenta.org/):HIM算法（层次时间记忆）
>* [pattern](http://www.clips.ua.ac.be/pattern):web挖掘
>* [Caffe](http://caffe.berkeleyvision.org/):视觉领域
>* [LibSVM](http://www.csie.ntu.edu.tw/~cjlin/libsvm/):针对SVM算法
>* [Nilearn](http://nilearn.github.io/):神经影像
>* [Statsmodels](http://statsmodels.sourceforge.net/):基于统计学
>* [PyMC](http://pymc-devs.github.io/pymc/README.html#purpose):贝叶斯统计模型，MCMC等。
>* [PYMVPA](http://www.pymvpa.org/):大数据的统计学习分析
>* [gensim](http://radimrehurek.com/gensim/):自然语言处理，主题模型
>* [featureforge](https://pypi.python.org/pypi/featureforge):专门用来构建或者测试特征的库。
>* [vaderSentiment](https://pypi.python.org/pypi/vaderSentiment):语义分析
