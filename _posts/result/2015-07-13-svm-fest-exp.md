---
layout: post
title: Liblinear/Boosting/Random Forest Classification Experiment Results
category: result
tags: Blog
keywords: svm,fest,boosting,random forest
description: Liblinear/Boosting/Random Forest Classification Experiment Results
---

> Test and compare the existing svm and boosting packages from two perspectives:
> 1. Training time and accuracy with different size of training set
> 2. Training time and accuracy with different size of feature
> 
> After the [experiment using adaboost and multiboost](http://localhost:4000/2015/07/12/bootsing-svm-exp.html), I've found another ensemble package ([FEST](http://lowrank.net/nikos/fest/)) for sparse high dimensional data.
> This package outperforms previous boosting packages both in training time and test accuracy. The corresponding paper seem to be [Caruana R, Karampatziakis N, Yessenalina A. An empirical evaluation of supervised learning in high dimensions[C]. *ICML*. ACM, 2008](http://icml2008.cs.helsinki.fi/papers/632.pdf)
> 

## 1. Different sample size

### 1.1 Descriptions
* Dataset: [rcv1.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#rcv1.binary)
    - Training set: Randomly sample 0.1, 0.2, ..., 1 among [rcv1_train.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary/rcv1_train.binary.bz2) to be the training set
    - Test set: Fixed subset (0.1 random sample) of [rcv1_test.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary/rcv1_test.binary.bz2)
* Measurement:
    * Prediction accuracy on test set
    * Training time 
* Parameters:
    * [Liblinear](http://www.csie.ntu.edu.tw/~cjlin/liblinear/): Use the -C option to find the best c using cross-validation, use the best c to train the model and report the training time and accuracy on the test set.
    * Boosting in [FEST](http://lowrank.net/nikos/fest/) Packages:
        - Maximum depth of the trees: **5** (when maximun depth is large, the training time is too long and the accuracy does not seem to be increaseing)
        - Rounds: 100
    * Random forest in [FEST](http://lowrank.net/nikos/fest/) Packages:
        - Maximum depth of the trees: **100** (random forest does not work so well when maximun depth is small)
        - Rounds (Number of trees): 100

### 1.2 Results

<h5>All</h5> 

![samplesize_lib_fest](http://7xk717.com1.z0.glb.clouddn.com/samplesize_lib_fest.png)

<h5>Liblinear</h5>
![samplesize_liblinear2](http://7xk717.com1.z0.glb.clouddn.com/samplesize_liblinear2.png)

<h5>Boosting in FEST</h5>
![samplesize_boosting](http://7xk717.com1.z0.glb.clouddn.com/samplesize_boosting.png)

<h5>Random Forest in FEST</h5>
![samplesize_randomforest](http://7xk717.com1.z0.glb.clouddn.com/samplesize_randomforest.png)

### 1.3 Conclusions and Analysis
* Liblinear still performs the best with the highest accuracy rate and minimum training time, followed by FEST random forest and FEST boosting.
* Test accuracy:
    * The test accuracy for all three algorithms are fairly closed to each other (within 2% difference). 
    * For all 3 algorithms, the test accuracy is converging. The increasing speed is relatively fast when sample size is smaller than 2k, and slows down afterwards.
* Training time:
    * Random Forest and Liblinear is much faster than boosting.
    * For Liblinear and Boosting, training time increases almost linearly with the growth of training sample size.
    * For Random Forest, the training time curve is slightly quadratic.
    * When sample size reaches 17k, training time for all 3 algorithms seems to be vibrating a little bit, especially liblinear. 

## 2. Different feature size

### 2.1 Descriptions
* Dataset: [rcv1.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#rcv1.binary)
    - Training set:
        * Randomly sample 0.3 among [rcv1_train.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary/rcv1_train.binary.bz2)
        * For each feature, calculate the p-value of the two-sample t-test between the positive and negative samples.
        * Sort features by desendant p-value
        * Select the first 0.1, 0.2, ..., 1 features to generate new training data
    - Test set:
        * Use one fixed test set: 0.1 sample from [rcv1_test.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary/rcv1_test.binary.bz2)
        * For each new training data, choose same features of the test set to generate new test data.
        
* Measurement:
    * Prediction accuracy on test set
    * Training time
* Parameters:
    * Same as previous section

### 2.2 Results

<h5>All</h5> 

![featuresize_lib_fest](http://7xk717.com1.z0.glb.clouddn.com/featuresize_lib_fest.png)

<h5>Liblinear</h5>
![featuresize_liblinear2](http://7xk717.com1.z0.glb.clouddn.com/featuresize_liblinear.png)

<h5>Boosting in FEST</h5>
![featuresize_boosting](http://7xk717.com1.z0.glb.clouddn.com/featuresize_boosting.png)

<h5>Random Forest in FEST</h5>
![featuresize_randomforest](http://7xk717.com1.z0.glb.clouddn.com/featuresize_randomforest.png)

### 2.3 Conclusions and Analysis
* Liblinear performs the best with the highest accuracy rate and minimum training time, followed by FEST random forest and FEST boosting.
* Test Accuracy:
    * Liblinear
        Test accuracy is converging. The increasing speed slows down when feature size reaches 5k
    * FEST boosting
        Test accuracy vibrates a little bit but still it stays the same for two periods and exhibits a small leap after feature size reaches 26k
    * FEST randomforest
        Test accuracy vibrates around 94.7% when feature size is bigger than 5k
* Training Time:
    * Liblinear
        Training time is converging intially, but when feature size reaches 26k it suddenly jumps up and then decreses gradually.
    * FEST boosting
        Training time is converging as a whole. But it presents a tiny leap when feature size reaches 26k.
    * FEST random forest
        Training time shakes a lot. It increases as a whole initially and falls down suddenly when feature size reaches 30k.
