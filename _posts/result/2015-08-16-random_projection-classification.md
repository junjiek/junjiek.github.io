---
layout: post
title: Random Projection Classification Experiment
category: result
tags: Blog
keywords: random projection,classification
description: Random Projection Classification Experiment
---

# Random Projection as Weak Classifier

I've implemented two weak classifiers:

**Random Projection Classifier** (Use Random Projection directly as weak claasifier):
1. Randomly project data to lower dimension;
2. Group projected samples by their maximum feature index;
3. Majority vote (using sample weights) to decide class label for each group. 

**Random Projection Decision Stump** (combines random projection with decision tree):
1. Randomly project data to the dimension suggested by the [Johnson Lindenstrauss Lemma](http://scikit-learn.org/stable/modules/generated/sklearn.random_projection.johnson_lindenstrauss_min_dim.html#sklearn.random_projection.johnson_lindenstrauss_min_dim)
2. Train a decision tree (or decision stump) on top of the projected data

I've also inserted these base classifiers into the Adaboost framework in scikit-learn.

### Dataset Information:
* [news20.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#news20.binary) (70% as training set, 30% as test set)
    - \# of class: 2
    - \# of instance: 13997 / 5999 (testing)
    - \# of features: 1355191
* [rcv1.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#rcv1.binary)
    - \# of class: 2
    - \# of instance: 14169 / 6073 (testing)
    - \# of features: 47236

## Result:

### 1. Different Random Projection Methods
When the dataset is large, [GaussianRandomProjection](http://scikit-learn.org/stable/modules/generated/sklearn.random_projection.GaussianRandomProjection.html#sklearn.random_projection.GaussianRandomProjection) will be much much more slower than [SparseRandomProjection](http://scikit-learn.org/stable/modules/generated/sklearn.random_projection.SparseRandomProjection.html#sklearn.random_projection.SparseRandomProjection). Therefore, if we aim to enhance speed, we'd better use sparse projection matrix. In that sense, I am afraid we cannot adaptively change the projection matrix (as previously I suggested to change it to the mean of the majority class).

### 2. Single Weak Classifier performance:
> The blue line is the accuracy of decision stump. The red triangle represents the projected dimension suggested by the [Johnson Lindenstrauss Lemma](http://scikit-learn.org/stable/modules/generated/sklearn.random_projection.johnson_lindenstrauss_min_dim.html#sklearn.random_projection.johnson_lindenstrauss_min_dim), which is only related to the number of sample and a parameter eps.

* [news20.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#news20.binary)
    * Testing accuracy ![](http://7xk717.com1.z0.glb.clouddn.com/rpnews20_binary_weak.png)
    * Training time: Note that when projected dimension is large, random projection will be more expensive than decision stump. ![](http://7xk717.com1.z0.glb.clouddn.com/rpnews20_binary_weak_time.png)

* [rcv1.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#rcv1.binary)
    * Testing accuracy ![](http://7xk717.com1.z0.glb.clouddn.com/rprcv1_binary_weak.png)
    * Training time: Note that when projected dimension is large, random projection will be more expensive than decision stump.. ![](http://7xk717.com1.z0.glb.clouddn.com/rprcv1_binary_weak_time.png)

<!-- ### 3. Decision Tree over Random Projected data
Grow a full tree over the projected data and compare it with the original full tree

* [news20.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#news20.binary)
    * Testing accuracy:
        * ![](http://7xk717.com1.z0.glb.clouddn.com/rpnews20_binary_tree.png)
    * Training time:
        * ![](http://7xk717.com1.z0.glb.clouddn.com/rpnews20_binary_tree_time.png)

* [rcv1.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#rcv1.binary)
    * Testing accuracy:
        * ![](http://7xk717.com1.z0.glb.clouddn.com/rprcv1_binary_tree.png)
    * Training time:
        * ![](http://7xk717.com1.z0.glb.clouddn.com/rprcv1_binary_tree_time.png) -->

### 3. Adaboost Random Projection 
Weak classifers:
1.  **Decision Stump (DS)**
2.  **Random Projection Classifier (RP)**
3.  **Random Projection Decision Stump (RPDS)** (Projected dimension is fixed to the one suggested by [Johnson Lindenstrauss Lemma](http://scikit-learn.org/stable/modules/generated/sklearn.random_projection.johnson_lindenstrauss_min_dim.html#sklearn.random_projection.johnson_lindenstrauss_min_dim), with eps = 0.1)

Boost three classifiers by 100, 200,500, 1000 rounds. Although single RPDS performs worse than single DS, the ensemble of RPDS shows best performance.

* [news20.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#news20.binary)
    * Testing accuracy: Boosting did not help much for this RandomProjectionClassifier.
        * ![](http://7xk717.com1.z0.glb.clouddn.com/rpada_news20_binary.png)
    * Training time: When projected dimension is large, random projection is more expensive than decision stump
        * ![](http://7xk717.com1.z0.glb.clouddn.com/rpada_news20_binary_time.png)

* [rcv1.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#rcv1.binary)
    * Testing accuracy:
        * ![](http://7xk717.com1.z0.glb.clouddn.com/rpada_rcv1_binary.png)
    * Training time:
        * ![](http://7xk717.com1.z0.glb.clouddn.com/rpada_rcv1_binary_time.png)


## Conclusions:
1. Random Projection is hard to be used directly as a weak classifier for ensemble. For the following reasons:
    * Random Projection Matrix is hard to be changed adaptively
    * Boosting did not help much for this weak classifier
2. Increase of projected dimension helps improve accuracy but lower speed. When projected dimension is too large, random projection takes longer time than decision stump
3. Ensemble of **Random Projection Decision Stump** seem to enhance accuracy as well as speed, compared with ensemble of simple decision stump. This is consistent with previous work, Random Projection helps improve diversity for tree classifiers.