---
layout: post
comments: true
title:  "Decision Tree"
title2:  "Decision Tree"
date:   2017-07-06 19:22:00
permalink: /decision-tree/
mathjax: true
tags: Statistics Machine-Learning Decision-Tree Supervised-Learning
categories: Statistics Machine-Learning
img: /blog/assets/decision-tree/decision-tree.png
summary: Decision tree is a prediction technique that uses a decision tree to go from explanatory variables (represented in the branches) to conclusions about the dependent variable (represented in the leaves)...
---


Decision tree is a prediction technique that uses a decision tree to go from explanatory variables (represented in the branches) to conclusions about the dependent variable (represented in the leaves).

## 1. Description
In a decision tree model:
* Each branch node is an explanatory variable. Each branch from that node represents a value or a value range of the variable.
* Each leaf node is a possible value of depdendent variable.

Decision tree can provide a set of rules to predict depdendent variable based on explanatory variables.
<div class="imgcap">
<div >
    <img src="/blog/assets/decision-tree/decision-tree.png" width = "400">
</div>
</div>

## 2. Math
We want to grow a decision tree that best predicts the dependent variable, by deciding:
* Which explanatory variable should be branched first?
* What is the best split to branch that explanatory variable?

We can answer these questions by measuring impurity before and after branching. Common impurity measures are:
* __GINI Index:__ represents purity at a node.
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

* __Entropy:__ represents impurity at a node.
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
GainRATIO_{split} = \frac{Gain_{split}}{splitINFO} \\\
splitINFO = -\sum_{i=1}^k \frac{n_i}{n} log(\frac{n_i}{n})
\\]

* __Misclassification Error:__
\\[
Error(t) = 1 - \max_j P(j|t) \\\
where ~P(j|t) ~is ~the ~relative ~frequency ~of ~class ~j ~at ~node ~t
\\]
Error at a node would have minimum value of 0 when the node only contains one class, and maximum value of \\(1-\frac{1}{C}\\) when the node contains equal number of records for each of C classes. We need to choose the split that result in the lowest error.

For binary classification, it does not matter which impurity measure is chosen since all three impurity measures result in the same splitting choice.
<div class="imgcap">
<div >
    <img src="/blog/assets/decision-tree/impurity.png" width = "400">
</div>
</div>

__Pre-prune__

To reduce overfitting, we usually stop branching a node in decision tree when:
* all the records at the node belong to the same class
* all records at the node have the same explanatory variables' value
* the number of records at the node is less than a certain threshold
* class distribution at the node are independent of the available features (e.g. using \\(\chi^2\\) test)
* branching the node does not improve impurity measures

__Post-prune__

An alternative approach is to grow a decision tree to its entirely and perform bottom-up pruning: At each node, compute generalization error  for keeping the subtree, and pruning the subtree by replacing it with a leaf node. If the generalization error is reduced by pruning, prune the subtree at the node.

There are many way to determine generalization error. Suppose E examples are classified incorrectly out of N training examples at a node, \\(\hat{p} = \frac{E}{N}\\) is observed error rate. True error rate can be estimated by the upper bound of confidence interval at a given sigificant level \\(\alpha\\), denoted by: 
\\[
U_{1-\alpha}(E, N)
\\]

If depdendent variable is binary, the upper bound of confidence interval of a binomial distribution variable at a given sigificant level can be approximated by:

\\[
\hat{p} + z_{1-\frac{\alpha}{2}} \sqrt{\frac{1}{N} \hat{p} (1-\hat{p})}
\\]

Generalization error at the node would be:
\\[
N*U_{1-\alpha}(E, N)
\\]


## 3. Random Forest
Random forest is a decision tree-based [ensemble technique](https://en.wikipedia.org/wiki/Ensemble_learning) that trains multiple indenpendent decision trees and combine their predictions to reducing the variance. Random forest starts with bagging to generate multiple training sets, then train decision trees on these training sets using subset of explanatory variables, then combine their predictions.
- Data Bagging: Given a standard training set \\(D\\) of size \\(n\\), random forest generates m new training sets \\(D_i\\), each of size \\(n'\\), by sampling from \\(D\\) uniformly and with replacement. Each of these training sets will be used to train a decision tree.
- Feature Bagging: At each candidate split in the training process, only a random subset of explanatory variables is selected for branching.
- Ensemble: combine predictions from these decision trees by simple voting.
<div class="imgcap">
<div >
    <img src="/blog/assets/decision-tree/random-forest.png" width = "400">
</div>
</div>

## 4. Boosted Tree
Boosted Tree is another ensemble technique that produces a prediction model by combining decision trees. Unlike random forest in which decision trees are trained independently, decision trees in gradient boosting are trained in a way that subsequent tree pays more attenton to mistakes made by previous tree in order to correct these mistakes.
