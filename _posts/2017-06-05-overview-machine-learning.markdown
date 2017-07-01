---
layout: post
comments: true
title:  "Machine Learning Overview"
title2:  "Machine Learning Overview"
date:   2017-06-05 15:22:00
permalink: /overview-machine-learning/
mathjax: true
tags: Overview Machine-Learning
categories: Overview Machine-Learning
img: /blog/assets/overview/machine-learning.jpg
summary: Machine Learning is a subfield of computer science that give computers the ability to learn from data without being explicitly programmed.
---


"Machine Learning is a subfield of computer science that give computers the ability to learn from data without being explicitly programmed."
Characteristics of machine learning techniques:
* Machine Learning techniques generally do not make any assumption of underlying data. A machine learning engineer might apply linear regression model on a data that follow Poisson distribution, but a statistician would not be happy about it.
* Machine Learning techniques focus on prediction rather than explanation or interpretation of data
* Machine Learning techniques usually formulate problem in terms of minimizing a cost function, and in doing so, we hope to achieve the best prediction.

## 1. Unsupervised Learning
* Clustering
  * Hierachical Clustering
  * [K-means](/blog/k-means/)
  * DBSCAN
  * Mixture Model
* Association Rule Mining
* Latent variable model
  * Principal Component Analysis
  * Singular Value Decomposition<!---  * Collaborative Filtering -->
* Neural Network
  * Autoencoder
  * Adversarial Learning

## 2. Supervised Learning
* [Linear Regression](/blog/linear-regression/)
* [Logistics Regression](/blog/logistic-regression/)
* [Support Vector Machine](/blog/svm/)
* [Decision Tree](/blog/decision-tree/)
* Neural Network
  * Convolutional Neural Network
  * Recurrent Neural Network
* Probabilistic Model
  * Bayesian network
  * Markov random field<!---  * Restricted Boltzmann machine -->

## 3. Reinforcement Learning

