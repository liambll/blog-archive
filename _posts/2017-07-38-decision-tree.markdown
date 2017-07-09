---
layout: post
comments: true
title:  "Decision Tree"
title2:  "Decision Tree"
date:   2017-07-08 19:22:00
permalink: /decision-tree/
mathjax: true
tags: Statistics Machine-Learning Decision-Tree Supervised-Learning
categories: Statistics Machine-Learning
img: /blog/assets/decision-tree/decision-tree.png
summary: Decision tree is a prediction technique that uses a decision tree to go from explanatory variables (represented in the branches) to conclusions about the dependent variable (represented in the leaves)...
---


Decision tree is a prediction technique that uses a decision tree to go from explanatory variables (represented in the branches) to conclusions about the dependent variable (represented in the leaves).

## 1. Model
In a decision tree model:
* Each branch node is an explanatory variable. Each branch from that node represents a value or a value range of the variable.
* Each leaf node is a possible value of depdendent variable.

Decision tree can provide a set of rules to predict depdendent variable based on explanatory variables.
<div class="imgcap">
<div >
    <img src="/blog/assets/decision-tree/decision-tree.png" width = "500">
</div>
</div>

## 2. Estimation
We want to have a decision tree that best predict the depdent variable, by deciding:
* Which explanatory variable should be branched first?
* What is the best split to branch that explanatory variable?

We can answer these questions by measuring impurity before and after branching. Common impurity measures are:
* _GINI Index:_ represent purity at a node.
\\[
GINI(t) = 1 - \sum_j P(j|t)^2 \\\
where ~P(j|t) ~is ~the ~relative ~frequency ~of ~class ~j ~at ~node ~t
\\]
GINI at a node would have minimum value of 0 when the node only contains one class, and maximum value of \\(1-\frac{1}{C}\\) when the node contains equal number of records for each of C classes. We need to choose the split that results in the lowest GINI. The GINI of splitting at node t into k branches would be:
\\[
GINI_{split} = \sum_{i=1}^k \frac{n_i}{n} GINI(i) \\\
where ~n ~is ~the ~number ~of ~records ~before ~spliting \\\
and ~n_i ~is ~the ~number ~of ~records ~at ~child ~i
\\]

* _Entropy:_ represent impurity at a node.
\\[
Entropy(t) = - \sum_j P(j|t) log(P(j|t)) \\\
where ~P(j|t) ~is ~the ~relative ~frequency ~of ~class ~j ~at ~node ~t
\\]
Entropy at a node would have minimum value of 0 when the node only contains one class, and maximum value of \\(log(C)\\) when the node contains equal number of records for each of C classes. We need to choose the split that result in the highest reduction in impurity, such reduction also known as _Information Gain_. The Information Gain of splitting at node t into k branches would be:

\\[
Gain_{split} = Entropy(t) - (\sum_{i=1}^k frac{n_i}{n} Entropy(i) \\\
where ~n ~is ~the ~number ~of ~records ~before ~spliting \\\
~n_i ~is ~the ~number ~of ~records ~at ~child ~i
\\]

Choosing split using Information Gain tends to result in large number of small partition. We usually use a penalized version of Information Gain called Gain Ratio, which is used in [C4.5 algorithm](https://en.wikipedia.org/wiki/C4.5_algorithm): 

\\[
GainRATIO_{split = \frac{Gain_{split}}{splitINFO} \\\
splitINFO = -\sum_{i=1}^k \frac{n_i}{n} log(\frac{n_i}{n})
\\]

* _Misclassification Error:_
\\[
Error(t) = 1 - \max_j P(j|t) \\\
where ~P(j|t) ~is ~the ~relative ~frequency ~of ~class ~j ~at ~node ~t
\\]
Error at a node would have minimum value of 0 when the node only contains one class, and maximum value of \\(1-\frac{1}{C}\\) when the node contains equal number of records for each of C classes. We need to choose the split that result in the highest reduction in Entropy, such reduction also known as _Information Gain_. The Information Gain of splitting at node t into k branches would be:
