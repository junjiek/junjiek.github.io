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

#### 1.2.1 Select by Information Gain

![rcv1_binary_ig](http://7xk717.com1.z0.glb.clouddn.com/rcv1_binary_ig.png)

#### 1.2.2 Select by CHI-square test

![rcv1_binary_chi](http://7xk717.com1.z0.glb.clouddn.com/rcv1_binary_chi.png)

#### 1.2.3 Select by t-test p-value 

![rcv1_binary_t](http://7xk717.com1.z0.glb.clouddn.com/rcv1_binary_t.png)

#### 1.2.4 Select by random

![rcv1_binary_r](http://7xk717.com1.z0.glb.clouddn.com/rcv1_binary_r.png)

#### 1.2.5 Compare random, IG, CHI^2, t-test
![rcv1_binary_cmp](http://7xk717.com1.z0.glb.clouddn.com/rcv1_binary_cmp.png)

-------

## 2. Sampled [real-sim](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#real-sim)

### 2.1 Info:
* \# of data: 36,155 / 36,154 (testing)
* \# of maximum features: 20,940

### 2.2 Result:

#### 2.2.1 Select by Information Gain

![realsim_ig](http://7xk717.com1.z0.glb.clouddn.com/realsim_ig.png)

#### 2.2.2 Select by CHI-square

![realsim_chi](http://7xk717.com1.z0.glb.clouddn.com/realsim_chi.png)

#### 2.2.3 Select by t-test p-value

![realsim_t](http://7xk717.com1.z0.glb.clouddn.com/realsim_all.png)

#### 2.2.4 Select by random

![realsim_r](http://7xk717.com1.z0.glb.clouddn.com/realsim_rall.png)

#### 2.2.5 Compare random, IG, CHI^2, t-test
![realsim_cmp](http://7xk717.com1.z0.glb.clouddn.com/realsim_cmp.png)

-------

## 3. [news20.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#news20.binary)

### 3.1 Info:
* \# of data: 9,998 / 9,998 (testing)
* \# of maximum features: 1,355,180

### 3.2 Result:

#### 3.2.1 Select by Information Gain

![news20_binary_ig](http://7xk717.com1.z0.glb.clouddn.com/news20_binary_ig.png)

#### 3.2.1 Select by CHI-square

![news20_binary_chi](http://7xk717.com1.z0.glb.clouddn.com/news20_binary_chi.png)

#### 3.2.1 Select by random

![news20_binary_r](http://7xk717.com1.z0.glb.clouddn.com/news20_binary_r.png)

#### 2.2.3 Compare random, IG, CHI^2
![news20_binary_cmp](http://7xk717.com1.z0.glb.clouddn.com/news20_binary_cmp.png)

-------

## 4. [gisette](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#gisette)

> Although this dataset is a small one, it takes a very long time to run. 

### 4.1 Info:
* \# of data: 6,100 / 1,000 (testing)
* \# of maximum features: 20,940

### 4.2 Result:

> This dataset has negative value which CHI-square in scikit-learn doesn't accept

#### 4.2.1 Select by Information Gain

![gisette_ig](http://7xk717.com1.z0.glb.clouddn.com/gisette_ig.png)

#### 4.2.2 Select by t-test p-value

![gisette_t](http://7xk717.com1.z0.glb.clouddn.com/gisette_t.png)

#### 4.2.3 Select by random

![gisette_r](http://7xk717.com1.z0.glb.clouddn.com/gisette_r.png)

#### 3.2.4 Compare random, IG, t-test
![gisette_cmp](http://7xk717.com1.z0.glb.clouddn.com/gisette_cmp.png)


-------


## 5. Sampled [url](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#url)

> This dataset has negative value which CHI-square in scikit-learn doesn't accept

### 5.1 Info:
* \# of data: 11,981 / 11,980 (testing)
* \# of maximum features: 3,231,920

### 5.2 Result:

#### 5.2.1 Select by Information Gain

![url_ig](http://7xk717.com1.z0.glb.clouddn.com/url_ig.png)

#### 5.2.2 Select by random

![url_r](http://7xk717.com1.z0.glb.clouddn.com/url_r.png)

#### 5.2.3 Compare random, IG
![url_cmp](http://7xk717.com1.z0.glb.clouddn.com/url_cmp.png)
