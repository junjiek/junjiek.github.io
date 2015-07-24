---
layout: post
title: Simple Comparison of State-of-art RandomForest, Boosted Trees Packages
category: tool
tags: Blog
keywords: randomForest,gbm,boosted tree,scikit-learn,packages,ensemble learning
description: simple comparison of State-of-art randomForest, boosted trees packages
---
> I've looked into some of the most widely used packages in random forest and boosted trees. Besides, I learned about how they tune parameters.
> Among those packages, only [Scikit-Learn](scikit-learn.org) ([RandomForestClassifier](http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)) in Python, [FEST](multiboost.org) in C sclaes well to high-dimensional problems
> Below is the detailed summary of those packages I tried

# 1.Random Forest Packages

## 1.0.Usual Parameters

For high dimensional classification problem, the parameters for random forest is usually
1) **Number of trees**: The larger the better. Often $$ntree = 500$$ is sufficient 
2) **Number of features sampled at each split** ($$ m_{try} $$): Default is $$ s = \sqrt{feature\ num} $$ and it may be worthwhile to try larger ones. Sometimes will do cross-validate to find the best (try $$ s/2 $$, $$ s $$, $$ 2s $$, $$ 4s $$, $$ 8s $$)

## 1.1.[randomForest](https://cran.r-project.org/web/packages/randomForest/index.html) in R

#### 1.1.1. Publications and descriptions
* [Fortran original](http://www.stat.berkeley.edu/~breiman/RandomForests) by [Breiman L. Random forests. Machine learning, 2001.](http://machinelearning202.pbworks.com/w/file/fetch/60606349/breiman_randomforests.pdf)
* R port by [Liaw A, Wiener M. Classification and regression by randomForest. R news, 2002.](ftp://131.252.97.79/Transfer/Treg/WFRE_Articles/Liaw_02_Classification%20and%20regression%20by%20randomForest.pdf)

#### 1.1.2.Experiment Result:

It does not support high-dimensional sparse matrix, therefore, all the data needs to be transformed to a dense matrix which results in low speed. The program crashes when handling [rcv1_train.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#rcv1.binary). It is unsuitable for doing high-dimensional classification.

## 1.2.Weka in java

#### 1.2.1.Experiment Result:

I tried to write code in java to load libsvm format [rcv1_train.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#rcv1.binary) using weka, but the program crashed with an OutOfMemoryError. It seems that weka.core.converters.LibSVMLoader loads and stores the data in dense format internally during the process of determining the number of attributes and generating the header. Only after this process is complete does the loader produce the final ARFF data in Weka's sparse format. I tried to convert rcv1 from libsvm to ARFF format, but failed because of the slow speed. After all ARFF is not good at handling sparse datasets.

I've also tried the GUI version of weka to load the data, but it did not response for a long time and seemed to be loading data forever.

## 1.3.[Scikit-Learn](scikit-learn.org) ([RandomForestClassifier](http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)) in Python

#### 1.3.1. Publications and Descriptions

* [Pedregosa F, Varoquaux G, Gramfort A, et al. Scikit-learn: Machine learning in Python[J]. The Journal of Machine Learning Research, 2011, 12: 2825-2830.](http://arxiv.org/pdf/1201.0490.pdf)
* Scikit-learn is a widely used machine learning toolboox in python and is competitive with or better in speed than weka. But it is less cited in paper work than weka. 

#### 1.3.2.Experiment Result:

Capable of handling sparse matrix and high-dimensional multiclass datasets with random forest. Easy to do cross-validation, calculate F-score etc. I've tried it on [rcv1_multiclass](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass.html#rcv1.multiclass) and [news20](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass.html#news20) and it is faster with about 4% bigger error rate than FEST package.

## 1.4.[FEST](http://lowrank.net/nikos/fest/)

> The package I used to generate first-stage result

#### 1.4.2.Experiment Result:
Works fine with large libsvm format datasets such as [rcv1_multiclass](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass.html#rcv1.multiclass) and [news20](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass.html#news20). But it only supports binary classification. I've finished writing code for it to enable multiclass classification using one-vs-all strategy (weights are assigned to make the dataset balanced). 

# 2. Boosted Trees

## 2.0.Usual Parameters

1) **Iteration Number**: usually large and sometimes will do validation to find the best one.
2) **Tree nodes or max_depth**: usually depth = 3-5 or nodes = 8 for large classification number, but will need to be tuned for best performance.

## 2.1 [GBM](https://cran.r-project.org/web/packages/gbm) package in R

Does not support sparse matrix and large dataset

## 2.2. [Scikit-Learn](scikit-learn.org) ([GradientBoostingClassifier](http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingClassifier.html)) in Python

Does not support sparse matrix.

## 2.3. [Multiboost](multiboost.org)

Supports large dataset and multiclass classification problem but slow. I tried it with some simple parameters on [mnist](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass.html#mnist) dataset and finished with 84% accuracy (92% reported in their paper). But when I tried it on [rcv1_multiclass](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass.html#rcv1.multiclass) and [news20](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass.html#news20) using the same parameter, it gives really low accuracy (only about 25%). Don't know wether it is the problem of my parameters...

## 2.4. [FEST](multiboost.org)

> See section 1.4