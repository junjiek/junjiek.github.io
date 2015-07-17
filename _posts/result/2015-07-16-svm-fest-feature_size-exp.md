---
layout: post
title: Liblinear/Boosting/Random Forest Classification Experiment Results2
category: Result
tags: Blog
keywords: svm,fest,boosting,random forest
description: Liblinear/Boosting/Random Forest Classification Experiment Results2
---

> Test Liblinear and FEST packages on more datasets using different number of features. All the datasets come from [LIBSVM](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/) website.
> For datasets with high-dimensional features (approximately above 50k), it is too expensive to sort features by p-value of t-test. So I just sampled features randomly.
> Data points are selected by dividing the interval into **20** equal parts.


## 1. Sampled [rcv1.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#rcv1.binary)

### 1.1 Info:
* \# of data: 6,072 / 67,739 (testing)
* \# of maximum features: 47200

### 1.2 Result:

#### 1.2.1 Choose by p-value ranking

All 
![rcv1_1](http://7xk717.com1.z0.glb.clouddn.com/rcv1_1.png)

Liblinear
![rcv1_2](http://7xk717.com1.z0.glb.clouddn.com/rcv1_2.png)

FEST boosting
![rcv1_3](http://7xk717.com1.z0.glb.clouddn.com/rcv1_3.png)

FEST random forest
![rcv1_4](http://7xk717.com1.z0.glb.clouddn.com/rcv1_4.png)


#### 1.2.1 Choose by random

All 
![rcv1_r1](http://7xk717.com1.z0.glb.clouddn.com/rcv1_r1.png)

Liblinear
![rcv1_r2](http://7xk717.com1.z0.glb.clouddn.com/rcv1_r2.png)

FEST boosting
![rcv1_r3](http://7xk717.com1.z0.glb.clouddn.com/rcv1_r3.png)

FEST random forest
![rcv1_r4](http://7xk717.com1.z0.glb.clouddn.com/rcv1_r4.png)

-------

## 2. [news20.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#news20.binary)

### 2.1 Info:
* \# of data: 9,998 / 9,998 (testing)
* \# of maximum features: 1,355,180

### 2.2 Result:

#### 2.2.1 Choose by random

All 
![news20_r1](http://7xk717.com1.z0.glb.clouddn.com/news20_r1.png)

Liblinear
![news20_r2](http://7xk717.com1.z0.glb.clouddn.com/news20_r2.png)

FEST boosting
![news20_r3](http://7xk717.com1.z0.glb.clouddn.com/news20_r3.png)

FEST random forest
![news20_r4](http://7xk717.com1.z0.glb.clouddn.com/news20_r4.png)
