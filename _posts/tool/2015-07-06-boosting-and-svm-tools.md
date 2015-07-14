---
layout: post
title: Boosting及SVM的工具使用总结
category: 工具
tags: Blog
keywords: svm,boosting,adaboost,multiboost
description: Boosting及SVM的工具使用总结
---
>Wanna compare the performance of ensemble methods with svm, here's a summary of the usage of some existing tools.

# Document datasets
* [Libsvm Datasets](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/)
    * [news20](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass.html#news20)
    * [news20.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#news20.binary)
    * [rcv1.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#rcv1.binary)

# Boosting

## [Multiboost](http://www.multiboost.org/)

资源：[下载链接](http://www.multiboost.org/download/MultiBoost-1.2.02.zip?attredirects=0&d=1)、[使用文档](http://docs.google.com/viewer?a=v&pid=sites&srcid=bXVsdGlib29zdC5vcmd8d3d3fGd4OjE5YjY0MzgwNjNlNjU1NmY)

使用方法：

    $ ./multiboost --stronglearner [AdaBoostMH/ArcGV/FilterBoost/VJcascade/SoftCascade]
                 --fileformat [arff/svmlight/simple]
                 --traintest <trainfile> <testfile> <iteration_num>
                 --verbose [0-5]
                 --learnertype SingleStumpLearner
                 --outputfile <results.dta>
                 --shypname shyp.xml

## [Adaboost](https://github.com/yamaguchi23/adaboost)

使用方法：
<h5>Training</h5>  

    $ ./abtrain [options] training_set_file [model_file]  
      options:  
        -t: type of boosting (0:discrete, 1:real, 2:gentle) [default:2]  
        -r: the number of rounds [default:100]  
        -v: verbose'

<h5>Prediction</h5>  
    $ ./abpredict [options] test_set_file model_file  
      options:  
        -o: output score file  
        -v: verbose'

## [Fest](http://lowrank.net/nikos/fest/)

使用方法
<h5>Training</h5>

    festlearn [options] data model
            Available options:
                -c <int>  : committee type:
                            1 bagging
                            2 boosting (default)
                            3 random forest
                -d <int>  : maximum depth of the trees (default: 1000)
                -e        : report out of bag estimates (default: no)
                -n <float>: relative weight for the negative class (default: 1)
                -p <float>: parameter for random forests: (default: 1)
                            (ratio of features considered over sqrt(features))
                -t <int>  : number of trees (default: 100)

<h5>Prediction</h5>

    festclassify [options] data model predictions
            Available options:
                 -t <int>  : number of trees to use (default: 0 = all)

# SVM

Documentation：（[Libsvm](http://www.csie.ntu.edu.tw/~cjlin/papers/guide/guide.pdf) [Liblinear](http://www.csie.ntu.edu.tw/~cjlin/papers/liblinear.pdf)）

## [Libsvm](http://www.csie.ntu.edu.tw/~cjlin/libsvm/index.html)

<h4>Procedure</h4>
* SVM formatting
* Scaling ( linearly to $$[−1, +1]$$ or $$[0, 1]$$ )
* Try the RBF kernel

$$ K(x, y)=e^{-\gamma ||x-y||^2} $$

* Use cross-validation to find the best parameter $$C$$ and $$\gamma$$
    * Try different pairs of $$(C, \gamma)$$ (grid-search)
* Use the best parameter $$C$$ and $$\gamma$$ to train the whole training set
* Test

<h4>Example</h4>>

> Scaled sets with default parameters

    $ ./svm-scale -l -1 -u 1 -s range3 svmguide3 > svmguide3.scale
    $ ./svm-scale -r range3 svmguide3.t > svmguide3.t.scale
    $ ./svm-train svmguide3.scale
    $ ./svm-predict svmguide3.t.scale svmguide3.scale.model svmguide3.t.predict

> Scaled sets with parameter selection

    $ python grid.py svmguide3.scale

> Using an automatic scrip

    $ python easy.py svmguide3 svmguide3.t

## [Liblinear](http://www.csie.ntu.edu.tw/~cjlin/liblinear/)

> Particularly useful for document data. ("bag-of-words" model)

> The -C option efficiently conducts cross validation several times and finds
the best parameter automatically.

    $ ./train -C -s 2 news20.scale

> Train and predict

    $ ./train -c 1 -s 2 trainfile modelfile
    $ ./predict testfile modelfile prediction

> The -q option disable verbose






