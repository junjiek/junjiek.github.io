---
layout: post
title: Liblinear/FEST Multilabel Classification Result
category: result
tags: Blog
keywords: svm,fest,scikit-learn,boosting,random forest
description: Liblinear/FEST Multilabel Classification Result
---

> Test Liblinear, scikit-learn, FEST on multi-class datasets, using different feature size. Report micro- and macro- F score.
> Information Gain, $$\chi^2$$-test, Random strategies are used to select different number of features, sample 20 times for each dataset. [scikit-learn feature selection tool box](http://scikit-learn.org/stable/modules/feature_selection.html) 

# ------------------- Multilabel Dataset ----------------

## Parameters:

* Liblinear: C = 1.0
* FEST Boosting: ntree = 100, max_depth = 5
* FEST Random Forest: ntree = 100, $$m_{try} = \sqrt{feature\ num}$$

## Method:
* Divide it into multiple binary classification problems.
* For each label, a clasifier is trained to predict +1 or -1.
    * I tried using SCut: leave 20% training data as validation set. Find the value of threshold that maximizes the F-score. But the result is bad on R21578 dataset. Seems that SCut tend to overfit
    * Currently, I just treat it as a multiclass problem, which means I train 2 classifiers (pos and neg). Use both clasifier to score the sample and choose the class with higher score.

## 1. Reuters-21578 ApteMode Version

### 1.1. Info:
* \# of classes: 90
* \# of data: 7,770 / 3,019 (testing)
* \# of features (original): 24240

### 1.2. Result:

#### 1.2.1. CHI-square

![r21578_chi_1](http://7xk717.com1.z0.glb.clouddn.com/r21578_chi_1.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/r21578_chi_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/r21578_chi_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/r21578_chi_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/r21578_chi_4.png),[SVM light](http://7xk717.com1.z0.glb.clouddn.com/r21578_chi_5.png)

#### 1.2.2. Information Gain

![r21578_ig_1](http://7xk717.com1.z0.glb.clouddn.com/r21578_ig_1.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/r21578_ig_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/r21578_ig_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/r21578_ig_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/r21578_ig_4.png),[SVM light](http://7xk717.com1.z0.glb.clouddn.com/r21578_ig_5.png)

<!-- #### 1.2.3. Random

![r21578_r](http://7xk717.com1.z0.glb.clouddn.com/r21578_r.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/r21578_r_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/r21578_r_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/r21578_r_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/r21578_r_4.png) -->

#### 1.2.4. Compare CHI, IG

![r21578_cmp](http://7xk717.com1.z0.glb.clouddn.com/r21578_cmp.png)


## 2. Subset of RCV1-v2 (Topics Category Set)

### 2.1. Info:
* \# of classes: 103
* \# of data: 23,149 / 39,063 (testing)
* \# of features (original): 47,236

### 2.2. Result:
> Boosting is too expensive to run because of the large number of classes and testing time. The result only contains Liblinear and FEST randomforest

#### 2.2.1. CHI-square

![rcv1_chi](http://7xk717.com1.z0.glb.clouddn.com/rcv1_chi.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/rcv1_chi_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/rcv1_chi_2.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/rcv1_chi_3.png)

#### 2.2.2. Information Gain

![rcv1_ig](http://7xk717.com1.z0.glb.clouddn.com/rcv1_ig.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/rcv1_ig_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/rcv1_ig_2.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/rcv1_ig_3.png)

#### 2.2.3. Random

![rcv1_r](http://7xk717.com1.z0.glb.clouddn.com/rcv1_r.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/rcv1_r_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/rcv1_r_2.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/rcv1_r_3.png)

#### 2.2.4. Compare CHI, IG, Random

![rcv1_cmp](http://7xk717.com1.z0.glb.clouddn.com/rcv1_cmp.png)

