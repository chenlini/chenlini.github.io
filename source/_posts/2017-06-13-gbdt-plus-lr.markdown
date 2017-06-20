---
layout: post
title: "GBDT+LR"
date: 2017-06-13 16:52:56 +0800
comments: true
categories: Algorithm
---
#GBDT+LR融合
##原理
工业界LR模型用的比较多的原因就是它非常容易可以并行化，处理起大规模的数据来比较容易。但是LR的学习能力有限，必须要经历大量的特征选择，特征组合等工作。因此找到合适的方法简化特征工程是非常重要的。facebook在KDD上发表了一篇文章，讲的就是GBDT+LR，为我们提供了一些思路，论文中的基本原理很简单，搞清楚下面这幅图就行了：

![](./images/屏幕快照 2017-06-13 16.41.39.png)

>1. 使用GBDT训练数据，得到如下2棵树，第一棵树3个叶子结点，第二棵树2个叶子结点，总共5个叶子结点。因此最后用于LR的特征向量就是5维的[0,0,0,0,0]。
>
>2. 训练数据共有n个样本，那么对于其中一个样本x,查看x最终会出现在哪些树的结点上面。比如x出现在树1的第1个结点以及树2的第2个结点，那么特征向量就是[1,0,0,0,1]
>得到的特征向量可以选择和原本的特征一起带入逻辑回归中，也可以单独作为特征进行学习。


##demo
sklearn分别实现了GBDT和LR的算法，所以做一个小例子测试融合算法是否会比原始的算法好。重点介绍方法，结果不确定，因为参数没有调到最优。

```
import numpy as np
from sklearn import ensemble
from sklearn import  datasets
from sklearn.linear_model import LogisticRegression
from sklearn.datasets import make_hastie_10_2
from sklearn.ensemble import GradientBoostingClassifier
```

######注意：Boosting的方法也分分类树和回归树，这里选择的是分类树，因为make\_hastie\_10\_2这个数据集是一个二分类的数据集

###单纯使用GradientBoostingClassifier
```
X, y = make_hastie_10_2(random_state=0)
X_train, X_test = X[:2000], X[2000:]
y_train, y_test = y[:2000], y[2000:]
clf = GradientBoostingClassifier(n_estimators=100, learning_rate=1.0,    max_depth=1, random_state=0).fit(X_train, y_train)
sum(clf.predict(X_test)==y_test)
```
最后一行是统计分类正确的数目，这里的结果是9130

####单纯使用LogisticRegression
```
paramsLr={ 'multi_class':'multinomial',
          'penalty':'l2','solver':'sag', 'tol':0.0001
          }
lr1 = LogisticRegression(C=1.0,solver='sag', max_iter=100,penalty='l2',
                             multi_class='multinomial',tol=0.0001)
lr1.fit(X_train, y_train)
sum(lr1.predict(X_test)==y_test)
```
最后一行是统计分类正确的数目，这里的结果是5149

####GBDT+LR融合
基于原理中介绍到的思想，需要将GBDT运行的结果转化为LR能够接受的数据结构。

```
def PreLR_GBDT(clf,Features):
    result=clf.apply(Features)[:,:,0]
    classT=np.zeros(result.shape[1]+1)
    for num in range(0,result.shape[1]):
        classT[num+1]=max(result[:,num])

    classT=classT.cumsum()
    classT=classT.astype(np.int32)

    M=np.zeros((result.shape[0],classT[-1]))

    for num in range(0, result.shape[0]):
        for num2 in range(0, result.shape[1]):
            M[num, classT[num2] + result[num][num2] - 1] = 1

    return M
```
有了上面的函数之后就可以再建立LR的模型了：

```
X_train_LR_GBDT=np.append(X_train,PreLR_GBDT(clf, X_train),axis=1)
X_test_LR_GBDT=np.append(X_test,PreLR_GBDT(clf, X_test),axis=1)

lr_GBDT = LogisticRegression(solver='sag', max_iter=100,penalty='l2',
                             multi_class='multinomial',tol=0.0001)
lr_GBDT.fit(X_train_LR_GBDT, y_train)

sum(lr_GBDT.predict(X_test_LR_GBDT)==y_test)
```

最后一行是统计分类正确的数目，这里的结果是9140，这里采用的是GBDT训练过后的feature和原始组合的方式，当然和可以不组合，直接用新的feature进行训练。

以上展示的是如何把GBDT与LR融合到一起，每个模型都没有进行调参，因此结果参考意义不大。



