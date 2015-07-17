---
layout: post
title: Adaboost/Multiboost/Liblinear Classification Experiment Results
category: result
tags: Blog
keywords: svm,boosting,adaboost,multiboost
description: Adaboost/Multiboost/Liblinear Classification Experiment Results
---

> Test and compare the existing svm and boosting packages from two perspectives:
> 1. Training time and accuracy with different size of training set
> 2. Training time and accuracy with different size of feature

## 1. Different sample size

### 1.1 Descriptions
* Dataset: [rcv1.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#rcv1.binary)
    - Training set: Randomly sample 0.1, 0.2, ..., 1 among [rcv1_train.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary/rcv1_train.binary.bz2) to be the training set
    - Test set: Fixed subset (0.1 random sample) of [rcv1_test.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary/rcv1_test.binary.bz2)
* Measurement:
    * Prediction accuracy on test set
    * Training time 
* Parameters:
    * Liblinear: Use the -C option to find the best c using cross-validation, use the best c to train the model and report the training time and accuracy on the test set.
    * Multiboost:
        - BaseLearner: SingleSparseStumpLearner (much faster than the SingleStumpLearner)
        - Rounds: 50
    * Adaboost:
        - Type: gentle
        - Rounds: 50


### 1.2 Results

<h5>All</h5> 

![samplesize_all](http://7xk717.com1.z0.glb.clouddn.com/samplesize_lib_ada_mul.png)

<h5>Liblinear</h5>

![samplesize_liblinear](http://7xk717.com1.z0.glb.clouddn.com/samplesize_liblinear.png)

<h5>Adaboost</h5> 

![samplesize_adaboost](http://7xk717.com1.z0.glb.clouddn.com/samplesize_adaboost.png)

<h5>Multiboost</h5> 
![samplesize_multiboost](http://7xk717.com1.z0.glb.clouddn.com/samplesize_multiboost.png)

### 1.3 Conclusions and Analysis
* Liblinear performs the best with the highest accuracy rate and minimum training time.
* For all 3 algorithms, the test accuracy is converging and the training time increases linearly with the growth of training sample size.
* For those two boosting algorithms
    * Adaboost performs better in prediction accuracy.
    * Multiboost takes less time to train, but it also seems to take more time to run the test especially when the test set is large. Though I did not record the testing time.

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

![featuresize_all](http://7xk717.com1.z0.glb.clouddn.com/featuresize_lib_ada_mul.png)

<h5>Liblinear</h5> 

![featuresize_liblinear](http://7xk717.com1.z0.glb.clouddn.com/featuresize_liblinear.png)

<h5>Adaboost</h5> 

![featuresize_adaboost](http://7xk717.com1.z0.glb.clouddn.com/featuresize_adaboost.png)

<h5>Multiboost</h5>

![featuresize_multiboost](http://7xk717.com1.z0.glb.clouddn.com/featuresize_multiboost.png)

### 2.3 Conclusions and Analysis
* Liblinear performs the best with the highest accuracy rate and minimum training time. Its test accuracy is converging. Its training time is converging intially, but when feature size reaches **26k** it suddenly jumps up and then decreses gradually.
* For those two boosting algorithms
    * training time grows linearly. For adaboost, training time vibrates when feature size is large.
    * **Test accuracy behaves like a step curve**, the accuracy remains almost **unchanged** for both algorithms initially, but when feature size reaches **26k**, it jumps up suddenly.
* It seems that interesting things have happened when feature size reaches 26k. Further examinations and experiments on other datasets are needed to find out the reasons. 