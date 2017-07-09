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


"Artificial neural networks (ANNs) are computing systems inspired by the biological neural networks that constitute animal brains." While regression and its generalized linear model such as logistics regression aims to capture lienar relationship, Neural Network is well-known for learning non-linear relationships without exlicitly specifying such relationships. A neural network model usually has better accuracy compared to linear models, but it lacks intepretability. Neural Network model can be used in both supervised learning, unsupervised, and reinforcement learning.

## 1. Model Description
Multilayer perceptron contains an input layer, an output layer, and one or more hidden layers:
* Output layer contains output units: \\(\mathbf{y} = [y_1, y_2, ..., y_k] \\) is a vector of k output units representing the dependent variable. For example, if we want to perform 10-class prediction, we can perform one-hot encoding with k = 10. That means if an output is class 7, it would have \\(y_7\\) = 1 and the remaining \\(y_i\\) are all 0.
* Input layer contains input units: \\(\mathbf{x} = [x_1, x_2, ..., x_D] \\) is a vector of D input units representing the explanatory variables. For example, in fraud detection, each input unit can represent one characteristics of a transaction. In image processing, each input unit can represent one pixel of an image. In natural language processing, each input unit can represent a word in a sentence.
* Hidden layers contains hidden units: The way hidden layers are organized represent network architecture, the simplest being multi-layer perceptron:
<div class="imgcap">
<div >
    <img src="/blog/assets/neural-network/mlp.jpg" width = "500">
</div>
</div>
In each hidden unit \\(z_i\\) at layer L of a multi-layer perceptron, an activation function \\(h\\) is applied on linear combination \\(a_i\\) of units from previous layer (L-1). If all hidden units at layer L are connected to all units at layer (L-1), layer L is called a fully-conencted layer. If the network has a huge number of hidden layers, it is called a deep network.
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
  * Rectified Linear Unit (ReLU): quicker convergence in training, less prone to vanishing gradient problem but prone to dead ReLU problem in deep network.
\\[
h(t) = max(0, t)
\\]
  * Maxout: less prone to vanishing gradient problem and no dead ReLU problem in deep network, but double the number of parameters.
\\[
z_i^{(L)} = \max_j (w_{ij}^{(L-1)} z_j^{(L-1)})
\\]
  
## 2. Model Training
We need to minimize the difference between the true output \\(y\\) and the predicted output \\(y*\\).

__Loss function__

Depend on the nature of depdendent variable, we should use suitable loss function to represent the difference \\(E_n\\):
* Square loss: for continious dependent variable \\(y\\)
\\[
E(\mathbf{w}) = \frac{1}{2}\sum_{i=1}^N (y\_i - \mathbf{\bar{x}\_i}\mathbf{w})^2
\\]

* Absolute loss: for continious dependent variable \\(y\\)
\\[
E(\mathbf{w}) = \sum_{i=1}^N \|y\_i - \mathbf{\bar{x}\_i}\mathbf{w}\|
\\]

* Cross-entropy loss: for categorical dependent variable \\(y\\) one-hot encoded as \\([y_1, y_2, ... y_J]\\)
\\[
E(\mathbf{w}) = -\sum_{i=1}^N \sum\_{j} y_j \log(P(y_j \| \mathbf{x}; \mathbf{w})) \\\
where ~ P(y_j \| \mathbf{x}; \mathbf{w}) = \frac{\exp (\mathbf{w\_{j}}^T\mathbf{x}) } {\sum_k \exp(\mathbf{w\_{k}}^T\mathbf{x}) }
\\]

* Hinge loss: for categorical dependent variable \\(y\\) one-hot encoded as \\([y_1, y_2, ... y_J]\\)
\\[
E(\mathbf{w}) = \sum_{n=1}^N \sum\_{j \neq y_n} \max(0, \Delta - \mathbf{w}\_y^T\mathbf{x} + \mathbf{w}\_j^T\mathbf{x})
\\]

__Regularization__

Regularization is important to reduce overfitting. Common regularization techniques are:
* L1: \\(L(W) = \lambda * \sum\|W\|\\)
* L2: \\(L(W) = \lambda * \sum W^2 \\)
* Elastic net:  \\(L(W) = \lambda * \sum(βW2 + W) \\)
* Max norm: force \\(||w||\_2 < c \\)
* Dropout: drop random units in previous layers before feeding to the next layer. This technique is specific for neural network.

__Parameter Estimates__
There is usually no closed form solution to minimize the loss function in neural network. Unlike loss function in regression and logistics regression where there is no local minima, neural network's loss function usually has local minima. Therefore, it is possible that if we train neural network mutltiple times, we would obtain different parameter estimates.

We rely on gradient descent to estimate parameters. The gradient is caculated from the output layer and back-propagated to previous layers using chain rule:
\\[
d_w_{ij} \equiv \frac{\partial E_n}{\partial w_{ij}^{(L-1)}} = \frac{\partial E_n}{\partial a_i^{(L)}} \frac{\partial a_i^{(L)}}{\partial w_{ij}^{(L-1)}} \\\
\frac{\partial a_i^{(L)}}{\partial w_{ij}^{(L-1)}} = z_j^{(L-1)}
\\]

\\[
\delta_i^{(L)} \equiv \frac{\partial E_n}{\partial a_i^{(L)}} = h'(a_i^{(L)}) \sum_k w_{ik}^{(L+1)} \delta_k^{(L+1)}
\\]

We can update parameter \\(w\\) using direct gradient \\(dw\\), momentum version, or per-parameter version:
* Direct gradient:
\\[
w = w - learning_rate * dw
\\]
* Momentum: the parameters will build up velocity in any direction that has consistent gradient
\\[
v = v * \mu - learning_rate * dw \\\
w = w + v
\\]
* Adagrad: the parameters that receive high gradients will have their effective learning rate reduced, while parameters that receive small or infrequent updates will have their effective learning rate increased
\\[
cache = cache + dw^2
w = w - learning_rate * dw / (\sqrt(cache) + \epsilon)
\\]
* RMSprop: similar with Adagrad with an attempt to reduce its aggressive, monotonically decreasing learning rate by making cache variable "leaky"
\\[
cache = decay_rate * cache + (1 - decay_rate) * dw^2
w = w - learning_rate * dw / (\sqrt(cache) + \epsilon)
\\]
* Adam: RMSprop with momentum
\\[
m = \beta1 * m + (1-\beta1) * dw
v = \beta2* v + (1-\beta2) * (dw^2)
x = x - learning_rate * m / (\sqrt(v) + \epsilon)
\\]
* Newton’s method: requires second order derivatives computation. This approach leads to very fast convergence compared to first-order gradient, but it is too computational expensive for deep network.


