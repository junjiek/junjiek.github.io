---
layout: post
title: Liblinear/Boosting/Random Forest Classification Experiment Results 2
category: result
tags: Blog
keywords: svm,fest,boosting,random forest
description: Liblinear/Boosting/Random Forest Classification Experiment Results 2
---

> Test Liblinear and FEST packages on more datasets using different number of features.

# Notes

* All the datasets come from [LIBSVM](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/) website.
* Data points are selected by dividing the interval into **20** equal parts.
* For datasets with high-dimensional features (approximately above 50k), it is too expensive to sort features by p-value of t-test. So I just sampled features randomly. 
    - Noticed that different strategy of choosing features will affect the performace, I also compared some of the datasets using both p-value ranking and random strategies.

# Results

## 1. Sampled [rcv1.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#rcv1.binary)

### 1.1 Info:
* \# of data: 6,072 / 67,739 (testing)
* \# of maximum features: 47,200

### 1.2 Result:

#### 1.2.1 Choose by p-value ranking

![rcv1_all](http://7xk717.com1.z0.glb.clouddn.com/rcv1_all.png)

#### 1.2.2 Choose by random

![rcv1_rall](http://7xk717.com1.z0.glb.clouddn.com/rcv1_rall.png)

#### 1.2.3 Compare ranking and random
![rcv1_cmp](http://7xk717.com1.z0.glb.clouddn.com/rcv1_cmp.png)

-------

## 2. Sampled [real-sim](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#real-sim)

### 2.1 Info:
* \# of data: 636,155 / 36,154 (testing)
* \# of maximum features: 20,940

### 2.2 Result:

#### 2.2.1 Choose by p-value ranking

![realsim_all](http://7xk717.com1.z0.glb.clouddn.com/realsim_all.png)


#### 2.2.2 Choose by random

![realsim_rall](http://7xk717.com1.z0.glb.clouddn.com/realsim_rall.png)

#### 2.2.3 Compare ranking and random
![realsim_cmp](http://7xk717.com1.z0.glb.clouddn.com/realsim_cmp.png)

-------

## 3. [gisette](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#gisette)

> Although this dataset is a small one, it takes a very long time to run. 

### 3.1 Info:
* \# of data: 6,100 / 1,000 (testing)
* \# of maximum features: 20,940

### 3.2 Result:

#### 3.2.1 Choose by p-value ranking

![gisette_all](http://7xk717.com1.z0.glb.clouddn.com/gisette_all.png)

#### 3.2.2 Choose by random

![gisette_rall](http://7xk717.com1.z0.glb.clouddn.com/gisette_rall.png)

#### 3.2.3 Compare ranking and random
![gisette_cmp](http://7xk717.com1.z0.glb.clouddn.com/gisette_cmp.png)

-------

## 4. [news20.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#news20.binary)

### 3.1 Info:
* \# of data: 9,998 / 9,998 (testing)
* \# of maximum features: 1,355,180

### 3.2 Result:

#### 3.2.1 Choose by random

![news20_rall](http://7xk717.com1.z0.glb.clouddn.com/news20_rall.png)

-------


## 5. Sampled [url](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#url)

### 4.1 Info:
* \# of data: 11,981 / 11,980 (testing)
* \# of maximum features: 3,231,920

### 4.2 Result:

#### 4.2.1 Choose by random

![url_rall](http://7xk717.com1.z0.glb.clouddn.com/url_rall.png)
