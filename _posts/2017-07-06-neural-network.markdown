---
layout: post
comments: true
title:  "Neural Network"
title2:  "Neural Network"
date:   2017-07-06 17:22:00
permalink: /neural-network/
mathjax: true
tags: Machine-Learning Neural-Network Supervised-Learning
categories: Machine-Learning
img: /blog/assets/neural-network/neural-network.png
summary: Artificial neural networks (ANNs) are computing systems inspired by the biological neural networks that constitute animal brains...
---


"Artificial neural networks (ANNs) are computing systems inspired by the biological neural networks that constitute animal brains." While regression and its generalized linear model such as logistics regression aims to capture lienar relationship, Neural Network is well-known for learning non-linear relationships without exlicitly specifying such relationships. A neural network model usually has better accuracy compared to linear models, but it lacks intepretation.

Neural Network model can be used in both supervised learning, unsupervised, and reinforcement learning. This post focuses on a simpliest form of neural network called Feedforward neural network, also known as multi-layer perceptron. Advanced neural network models such as autoencoder, convolution neural network and recurrent neural network will be discussed in separate posts.

## 1. Model:
Feedforward neural network contains an input layer, an output layer, and one or more hidden layers in between:
<div class="imgcap">
<div >
    <img src="/blog/assets/neural-network/mlp.jpg" width = "500">
</div>
</div>
* Output layer contain output units: \\(\mathbf{y} = [y_1, y_2, ..., y_k] \\) is a vector of k output units representing the dependent variable. For example, if we want to perform 10-class prediction, we can perform one-hot encoding with k = 10. That means if an output is class 7, it would have \\(y_7\\) = 1 and the remaining \\(y_i\\) are all 0.
* Input layer contains input units: \\(\mathbf{x} = [x_1, x_2, ..., x_D] \\) is a vector of D input units representing the explanatory variables. For example, in fraud detection, each input unit can represent one characteristics of a transaction. In image processing, each input unit can represent one pixel of an image. 
* Hidden layers contains hidden units: In each hidden unit \\(z_i\\) at layer L, an activation function \\(h\\) is applied on linear combination \\(a_i\\) of units from previous layer (L-1):
//[
z_i^{(L)} = h(a_i^{(L)} \\\
a_i^{(L)} = \sum_j w_{ij}^{(L-1)} z_j^{(L-1)}
//]
Activation functions are usually non-linear. Some common activation functions are:
  * Sigmoid
  * Hyperbolic Tangent
  * Rectified Linear Unit (ReLU)

