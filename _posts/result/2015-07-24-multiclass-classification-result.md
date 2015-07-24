---
layout: post
title: Liblinear/Scikit-learn/FEST Multiclass Classification Result
category: result
tags: Blog
keywords: svm,fest,scikit-learn,boosting,random forest
description: Liblinear/Scikit-learn/FEST Multiclass Classification Result
---

> Test Liblinear, scikit-learn, FEST on multi-class datasets, using different feature size. Report micro- and macro- F score.
> $$\chi^2$$-test is used to select different number of features, sample 20 times for each dataset. [scikit-learn feature selection tool box](http://scikit-learn.org/stable/modules/feature_selection.html) 

# Parameters:

* Liblinear: cross validate to find best C
* FEST Boosting: ntree = 100, max_depth = 5
* FEST Random Forest: ntree = 100, $$m_{try} = \sqrt{feature\ num}$$
* Scikit-Learn Random Forest: ntree = 100, $$m_{try} = \sqrt{feature\ num}$$

# [rcv1.multiclass](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass.html#rcv1.multiclass)

### Info:
* \# of classes: 53
* \# of data: 15,564 / 518,571 (testing)
* \# of features (original): 47,236

### Result:

All

![rcv1_multi](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi.png)

Bigger Ones

![rcv1_multi_1](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_1.png)
![rcv1_multi_2](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_2.png)
![rcv1_multi_3](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_3.png)
![rcv1_multi_4](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_4.png)
![rcv1_multi_5](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_5.png)

# [news20](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass.html#news20)

### Info:
* \# of classes: 20
* \# of data: 15,935 / 3,993 (testing)
* \# of features (original): 62,061 / 62,060 (testing)

### Result:

All

![news20](http://7xk717.com1.z0.glb.clouddn.com/news20.png)

Bigger Ones

![news20_1](http://7xk717.com1.z0.glb.clouddn.com/news20_1.png)
![news20_2](http://7xk717.com1.z0.glb.clouddn.com/news20_2.png)
![news20_3](http://7xk717.com1.z0.glb.clouddn.com/news20_3.png)
![news20_4](http://7xk717.com1.z0.glb.clouddn.com/news20_4.png)
![news20_5](http://7xk717.com1.z0.glb.clouddn.com/news20_5.png)

