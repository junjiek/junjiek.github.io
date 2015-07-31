---
layout: post
title: Summary of Boosting and SVM tools
category: tool
tags: Blog
keywords: svm,boosting,adaboost,multiboost
description: Summary of Boosting and SVM tools
---
>Wanna compare the performance of ensemble methods with svm, here's a summary of the usage of some existing tools.

# Document datasets
* [Libsvm Datasets](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/)
    * [news20](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/multiclass.html#news20)
    * [news20.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#news20.binary)
    * [rcv1.binary](http://www.csie.ntu.edu.tw/~cjlin/libsvmtools/datasets/binary.html#rcv1.binary)

# Boosting

## [Multiboost](http://www.multiboost.org/)

Resource: [Download](http://www.multiboost.org/download/MultiBoost-1.2.02.zip?attredirects=0&d=1)、[Documentation](http://docs.google.com/viewer?a=v&pid=sites&srcid=bXVsdGlib29zdC5vcmd8d3d3fGd4OjE5YjY0MzgwNjNlNjU1NmY)

Usage:

    $ ./multiboost --stronglearner [AdaBoostMH/ArcGV/FilterBoost/VJcascade/SoftCascade]
                 --fileformat [arff/svmlight/simple]
                 --traintest <trainfile> <testfile> <iteration_num>
                 --verbose [0-5]
                 --learnertype SingleStumpLearner
                 --outputfile <results.dta>
                 --shypname shyp.xml

## [Adaboost](https://github.com/yamaguchi23/adaboost)

Usage:
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

Usage:
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

## [randomForest](https://cran.r-project.org/web/packages/randomForest/index.html) in R

#### Usage:
Install R

    ## MacOS  (https://cran.r-project.org/bin/macosx/)
    ## Linux  (https://cran.r-project.org/bin/linux/ubuntu/)
        $ sudo apt-get update
        $ sudo apt-get install r-base 
        $ sudo apt-get install r-base-dev

Install randomForest package
  
    ## install.packages("mypkg", lib="/my/own/path/to/R-packages/")
    > install.packages("randomForest")
    > insatll.packages("Hmisc")
  
Default Parameters for randomForest

    ## S3 method for class 'formula':
    > randomForest((formula, data=NULL, ..., subset, na.action=na.fail))

    ## S3 method for class 'default':
    > randomForest((x, y=NULL,  xtest=NULL, ytest=NULL, ntree=500,
                    mtry=if (!is.null(y) && !is.factor(y))
                    max(floor(ncol(x)/3), 1) else floor(sqrt(ncol(x))),
                    replace=TRUE, classwt=NULL, cutoff, strata,
                    sampsize = if (replace) nrow(x) else ceiling(.632*nrow(x)),
                    nodesize = if (!is.null(y) && !is.factor(y)) 5 else 1,
                    maxnodes = NULL,
                    importance=FALSE, localImp=FALSE, nPerm=1,
                    proximity, oob.prox=proximity,
                    norm.votes=TRUE, do.trace=FALSE,
                    keep.forest=!is.null(y) && is.null(xtest), corr.bias=FALSE,
                    keep.inbag=FALSE, ...))

    ## S3 method for class 'randomForest':
    > print((x, ...))

## 1.3.Weka in java

#### Usage: Add weka.jar to project; 

    RandomForest m_classifier = new RandomForest();
    m_classifier.setNumFeatures(100);
    File inputFile = new File("path/to/file");
    LibSVMLoader libsvm = new LibSVMLoader();
    libsvm.setFile(inputFile);
    Instances instancesTrain = libsvm.getDataSet();
    // ---- convert the first row to nomial (do classification) ----
    NumericToNominal convert= new NumericToNominal();
    String[] options= new String[2];
    options[0]="-R";
    options[1]="1";  //range of variables to make numeric
    onvert.setOptions(options);
    convert.setInputFormat(instancesTrain);
    instancesTrain=Filter.useFilter(instancesTrain, convert);
    // --------------------
    instancesTrain.setClassIndex(0);
    m_classifier.buildClassifier(instancesTrain);
    m_classifier.classifyInstance(instancesTest.instance(i)

## Scikit-Learn ([RandomForestClassifier](http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)) in Python

#### Usage

    from sklearn.datasets import load_svmlight_files
    from sklearn.ensemble import RandomForestClassifier
    
    def randomForest(trainfilename, testfilename):
        X_train, y_train, X_test, y_test = load_svmlight_files((trainfilename, testfilename))
        clf = RandomForestClassifier(n_estimators = 100)
        clf = clf.fit(X_train, y_train)
        y_predicted = clf.predict(X_test)
        y_pred = clf.predict(X_test)
        macro = f1_score(y_test, y_pred, average='macro')
        micro = f1_score(y_test, y_pred, average='micro')
        print 'micro:', micro, ', macro:', macro


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






