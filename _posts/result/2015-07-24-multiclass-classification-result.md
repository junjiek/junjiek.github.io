---
layout: post
title: Liblinear/Scikit-learn/FEST Multilabel/Multiclass Classification Result
category: result
tags: Blog
keywords: svm,fest,scikit-learn,boosting,random forest
description: Liblinear/Scikit-learn/FEST Multiclass Classification Result
---

> Test Liblinear, scikit-learn, FEST on multi-class datasets, using different feature size. Report micro- and macro- F score.
> Information Gain, $$\chi^2$$-test, Random strategies are used to select different number of features, sample 20 times for each dataset. [scikit-learn feature selection tool box](http://scikit-learn.org/stable/modules/feature_selection.html) 

# ------------------- Multilabel Dataset ----------------

## Parameters:

* Liblinear: C = 1.0
* FEST Boosting: ntree = 100, max_depth = 5
* FEST Random Forest: ntree = 100, $$m_{try} = \sqrt{feature\ num}$$
* Scikit-Learn Random Forest: ntree = 100, $$m_{try} = \sqrt{feature\ num}$$

## Multilabel Method:
* Divide it into multiple binary classification problems.
* For each label, a clasifier is trained to predict +1 or -1.
    * I tried using SCut: leave 20% training data as validation set. Find the value of threshold that maximizes the F-score. But the result is bad on R21578 dataset. Seems that SCut tend to overfit
    * Currently, I just treat it as a multiclass problem, which means I train 2 classifiers (pos and neg). Use both clasifier to score the sample and choose the class with higher score.

## 1. Subset of RCV1 (Topics Category Set)

### 1.1. Info:
* \# of classes: 103
* \# of data: 23,149 / 39,063 (testing)
* \# of features (original): 47,236

### 1.2. Result:
> Boosting is too expensive to run because of the large number of classes and testing time. The result only contains Liblinear and FEST randomforest

#### 1.2.1. CHI-square

![rcv1_chi](http://7xk717.com1.z0.glb.clouddn.com/rcv1_chi.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/rcv1_chi_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/rcv1_chi_2.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/rcv1_chi_3.png)

#### 1.2.2. Information Gain

![rcv1_ig](http://7xk717.com1.z0.glb.clouddn.com/rcv1_ig.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/rcv1_ig_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/rcv1_ig_2.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/rcv1_ig_3.png)

#### 1.2.3. Random

![rcv1_r](http://7xk717.com1.z0.glb.clouddn.com/rcv1_r.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/rcv1_r_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/rcv1_r_2.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/rcv1_r_3.png)

#### 1.2.4. Compare CHI, IG, Random

![rcv1_cmp](http://7xk717.com1.z0.glb.clouddn.com/rcv1_cmp.png)

## 2. Reuters-21578 ApteMode Version

### 2.1. Info:
* \# of classes: 90
* \# of data: 7,770 / 3,019 (testing)
* \# of features (original): 24240

### 2.2. Result:

#### 2.2.1. CHI-square

![r21578_chi](http://7xk717.com1.z0.glb.clouddn.com/r21578_chi.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/r21578_chi_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/r21578_chi_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/r21578_chi_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/r21578_chi_4.png)

#### 2.2.2. Information Gain

![r21578_ig](http://7xk717.com1.z0.glb.clouddn.com/r21578_ig.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/r21578_ig_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/r21578_ig_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/r21578_ig_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/r21578_ig_4.png)

#### 2.2.3. Random

![r21578_r](http://7xk717.com1.z0.glb.clouddn.com/r21578_r.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/r21578_r_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/r21578_r_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/r21578_r_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/r21578_r_4.png)

#### 2.2.4. Compare CHI, IG, Random

![r21578_cmp](http://7xk717.com1.z0.glb.clouddn.com/r21578_cmp.png)


# ------------------- Multiclass Dataset ----------------

## Parameters:

* Liblinear: cross validate to find best C
* FEST Boosting: ntree = 100, max_depth = 5
* FEST Random Forest: ntree = 100, $$m_{try} = \sqrt{feature\ num}$$
* Scikit-Learn Random Forest: ntree = 100, $$m_{try} = \sqrt{feature\ num}$$

## 1. [rcv1.multiclass](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass.html#rcv1.multiclass)

### 1.1. Info:
* \# of classes: 53
* \# of data: 15,564 / 518,571 (testing)
* \# of features (original): 47,236

### 1.2. Result:

#### 1.2.1. CHI-square

![rcv1_multi_chi](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_chi.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_chi_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_chi_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_chi_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_chi_4.png),[Sklearn RF](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_chi_5.png)

#### 1.2.2. Information Gain

![rcv1_multi_ig](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_ig.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_ig_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_ig_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_ig_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_ig_4.png),[Sklearn RF](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_ig_5.png)

#### 1.2.3. Random

![rcv1_multi_r](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_r.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_r_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_r_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_r_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_r_4.png),[Sklearn RF](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_r_5.png)

#### 1.2.4. Compare CHI, IG, Random

![rcv1_multi_cmp](http://7xk717.com1.z0.glb.clouddn.com/rcv1_multi_cmp.png)


## 2. [news20](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass.html#news20)

### 2.1. Info:
* \# of classes: 20
* \# of data: 15,935 / 3,993 (testing)
* \# of features (original): 62,061 / 62,060 (testing)

### 2.2. Result:

#### 2.2.1. CHI-square

![news20_multi_chi](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_chi.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_chi_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_chi_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_chi_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_chi_4.png),[Sklearn RF](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_chi_5.png)

#### 2.2.2. Information Gain

![news20_multi_ig](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_ig.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_ig_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_ig_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_ig_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_ig_4.png),[Sklearn RF](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_ig_5.png)

#### 2.2.3. Random

![news20_multi_r](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_r.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_r_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_r_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_r_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_r_4.png),[Sklearn RF](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_r_5.png)

#### 2.2.4. Compare CHI, IG, Random

![news20_multi_cmp](http://7xk717.com1.z0.glb.clouddn.com/news20_multi_cmp.png)

## 3. [sector](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass.html#sector)

### 3.1. Info:
* \# of classes: 105
* \# of data: 6,412 / 3,207 (testing)
* \# of features: 55,197 / 55,197 (testing)

### 3.2. Result:

#### 3.2.1. CHI-square

![sector_chi](http://7xk717.com1.z0.glb.clouddn.com/sector_chi.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/sector_chi_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/sector_chi_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/sector_chi_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/sector_chi_4.png),[Sklearn RF](http://7xk717.com1.z0.glb.clouddn.com/sector_chi_5.png)

#### 3.2.2. Information Gain

![sector_ig](http://7xk717.com1.z0.glb.clouddn.com/sector_ig.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/sector_ig_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/sector_ig_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/sector_ig_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/sector_ig_4.png),[Sklearn RF](http://7xk717.com1.z0.glb.clouddn.com/sector_ig_5.png)

#### 3.2.3. Random

![sector_r](http://7xk717.com1.z0.glb.clouddn.com/sector_r.png)

* Bigger Ones: [All](http://7xk717.com1.z0.glb.clouddn.com/sector_r_1.png), [Liblinear](http://7xk717.com1.z0.glb.clouddn.com/sector_r_2.png),[FEST BT](http://7xk717.com1.z0.glb.clouddn.com/sector_r_3.png),[FEST RF](http://7xk717.com1.z0.glb.clouddn.com/sector_r_4.png),[Sklearn RF](http://7xk717.com1.z0.glb.clouddn.com/sector_r_5.png)

#### 3.2.4. Compare CHI, IG, Random

![sector_cmp](http://7xk717.com1.z0.glb.clouddn.com/sector_cmp.png)

