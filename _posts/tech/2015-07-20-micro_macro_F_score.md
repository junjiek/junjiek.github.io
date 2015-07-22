---
layout: post
title: Micro and Macro F-score for multi-class classification
category: tech
tags: Blog
keywords: micro,macro,f-score,multi-class,classification
description: Micro and Macro F-score for multi-class classification
---

## Single Class: Precision, Recall, F1-score

$$ Precision = \frac{TP}{TP+FP}, Recall = \frac{TP}{TP+FN}, F_1\ score = 2*\frac{PR}{P+R} $$

## Multi-class: Micro-average, Macro-average ($$|C|$$ classes)

### Micro

$$P_{micro}=\frac{\sum^{|C|}_{i=1}TP_{i}}{\sum^{|C|}_{i=1}TP_{i}+FP_{i}}, R_{micro}=\frac{\sum^{|C|}_{i=1}TP_{i}}{\sum^{|C|}_{i=1}TP_{i}+FN_{i}}$$


$$ F(micro\ average)  = 2*\frac{P_{micro}R_{micro}}{P_{micro} + R_{micro}}$$

$$In\ single\ label\ question, P_{micro} = R_{micro} ?? $$


### Macro

$$ F_i = 2*\frac{P_i R_i}{P_i + R_i}$$

$$ F(macro\ average)  = \frac{\sum^{|C|}_{i=1}F_i}{|C|}$$


