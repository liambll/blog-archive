---
layout: post
comments: true
title:  "Neural Network"
title2:  "Neural Network"
date:   2017-06-30 17:22:00
permalink: /neural-network/
mathjax: true
tags: Machine-Learning Neural-Network Supervised-Learning
categories: Machine-Learning
img: /blog/assets/neural-network/neural-network.png
summary: Artificial neural networks (ANNs) are computing systems inspired by the biological neural networks that constitute animal brains...
---


"Artificial neural networks (ANNs) are computing systems inspired by the biological neural networks that constitute animal brains." While regression and its generalized linear model such as logistics regression aims to capture lienar relationship, Neural Network is well-known for learning non-linear relationships without exlicitly specifying such relationships. A neural network model usually has better accuracy compared to linear models, but it lacks intepretability.

Neural Network model can be used in both supervised learning, unsupervised, and reinforcement learning. There are various neural network architectures. Some commonly used architectures are:
* Multilayer perceptron: the simpliest form of neural network, which will be desribed in this post.
* Convolution neural network
* Recurrent neural network

## 1. Model Description
Multilayer perceptron contains an input layer, an output layer, and one or more hidden layers in between:
<div class="imgcap">
<div >
    <img src="/blog/assets/neural-network/mlp.jpg" width = "500">
</div>
</div>
* Output layer contains output units: \\(\mathbf{y} = [y_1, y_2, ..., y_k] \\) is a vector of k output units representing the dependent variable. For example, if we want to perform 10-class prediction, we can perform one-hot encoding with k = 10. That means if an output is class 7, it would have \\(y_7\\) = 1 and the remaining \\(y_i\\) are all 0.
* Input layer contains input units: \\(\mathbf{x} = [x_1, x_2, ..., x_D] \\) is a vector of D input units representing the explanatory variables. For example, in fraud detection, each input unit can represent one characteristics of a transaction. In image processing, each input unit can represent one pixel of an image. 
* Hidden layers contains hidden units: In each hidden unit \\(z_i\\) at layer L, an activation function \\(h\\) is applied on linear combination \\(a_i\\) of units from previous layer (L-1):
\\[
z_i^{(L)} = h(a_i^{(L)} \\\
a_i^{(L)} = \sum_j w_{ij}^{(L-1)} z_j^{(L-1)}
\\]
Activation functions are usually non-linear. Some common activation functions are:
  * Sigmoid: computation intensive due to exponential component, prone to vanishing gradient problem in deep network.
  \\[
h(t) = \frac{1}{1 + e^{-t}}
\\]
  * Hyperbolic Tangent: still prone to vanishing gradient problem in deep network.
\\[
h(t) = tanh(t)
\\]
  * Rectified Linear Unit (ReLU): quicker convergence in training, less to vanishing gradient problem in deep network.
\\[
h(t) = max(0, t)
\\]
  * Maxout:
\\[
z_i^{(L)} = \max_j (w_{ij}^{(L-1)} z_j^{(L-1)})
\\]
  
## 2. Model Training
We need to minimize the difference between the true output and the predicted output. Depend on the nature of depdendent variable, we should use suitable loss function to represent the difference \\(E_n\\):
* For continious dependent variable: square error or absolute error
* For categorical depdendent variable: hinge loss or cross-entropy loss

There is usually no closed form solution to minimize the loss function in neural network. Unlike loss function in regression and logistics regression where there is no local minima, neural network's loss function usually has local minima. Therefore, it is possible that if we train neural network mutltiple times, we would obtain different parameter estimates.

We rely on gradient descent to estimate parameters. The gradient is caculated from the output layer and back-propagated to previous layers using chain rule:
\\[
\frac{\partial E_n}{\partial w_{ij}^{(L-1)}} = \frac{\partial E_n}{\partial a_i^{(L)}} \frac{\partial a_i^{(L)}}{\partial w_{ij}^{(L-1)}} \\\
\frac{\partial a_i^{(L)}}{\partial w_{ij}^{(L-1)}} = z_j^{(L-1)}
\\]

\\[
\delta_i^{(L)} \equiv \frac{\partial E_n}{\partial a_i^{(L)}} = h'(a_i^{(L)}) \sum_k w_{ik}^{(L+1)} \delta_k^{(L+1)}
\\]

