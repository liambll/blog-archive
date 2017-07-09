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
* __Output layer:__ contains output units \\(\mathbf{y} = [y_1, y_2, ..., y_k] \\), a vector of k output units representing the dependent variable. For example, if we want to perform 10-class prediction, we can perform one-hot encoding with k = 10. That means if an output is class 7, it would have \\(y_7\\) = 1 and the remaining \\(y_i\\) are all 0.
* __Input layer:__ contains input units \\(\mathbf{x} = [x_1, x_2, ..., x_D] \\), a vector of D input units representing the explanatory variables. For example, in fraud detection, each input unit can represent one characteristics of a transaction. In image processing, each input unit can represent one pixel of an image. In natural language processing, each input unit can represent a word in a sentence.
* __Hidden layers:__ contain hidden units. The way hidden layers are organized represent network architecture, the simplest being __multi-layer perceptron__ (MLP):
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
  * __Sigmoid:__ computation intensive due to exponential component, prone to vanishing gradient problem in deep network.
  \\[
h(t) = \frac{1}{1 + e^{-t}}
\\]
  * __Hyperbolic Tangent:__ still prone to vanishing gradient problem in deep network.
\\[
h(t) = tanh(t)
\\]
  * __Rectified Linear Unit (ReLU):__ quicker convergence in training, less prone to vanishing gradient problem but prone to dead ReLU problem in deep network.
\\[
h(t) = max(0, t)
\\]
  * __Maxout:__ less prone to vanishing gradient problem and no dead ReLU problem in deep network, but double the number of parameters.
\\[
z_i^{(L)} = \max_j (w_{ij}^{(L-1)} z_j^{(L-1)})
\\]
  
## 2. Model Training
We need to minimize the difference between the true output \\(y\\) and the predicted output \\(y*\\).

__Loss function__

Depend on the nature of depdendent variable, we should use suitable loss function to represent the difference \\(E_n\\):
* __Square loss:__ for continious dependent variable \\(y\\)
\\[
E(\mathbf{w}) = \frac{1}{2}\sum_{i=1}^N (y\_i - \mathbf{\bar{x}\_i}\mathbf{w})^2
\\]

* __Absolute loss:__ for continious dependent variable \\(y\\)
\\[
E(\mathbf{w}) = \sum_{i=1}^N \|y\_i - \mathbf{\bar{x}\_i}\mathbf{w}\|
\\]

* __Cross-entropy loss:__ for categorical dependent variable \\(y\\) one-hot encoded as \\([y_1, y_2, ... y_J]\\)
\\[
E(\mathbf{w}) = -\sum_{i=1}^N \sum\_{j} y_j \log(P(y_j \| \mathbf{x}; \mathbf{w})) \\\
where ~ P(y_j \| \mathbf{x}; \mathbf{w}) = \frac{\exp (\mathbf{w\_{j}}^T\mathbf{x}) } {\sum_k \exp(\mathbf{w\_{k}}^T\mathbf{x}) }
\\]

* __Hinge loss:__ for categorical dependent variable \\(y\\) one-hot encoded as \\([y_1, y_2, ... y_J]\\)
\\[
E(\mathbf{w}) = \sum_{n=1}^N \sum\_{j \neq y_n} \max(0, \Delta - \mathbf{w}\_y^T\mathbf{x} + \mathbf{w}\_j^T\mathbf{x})
\\]

__Regularization__

Regularization is important to reduce overfitting. Common regularization techniques are:
* __L1:__ \\(L(W) = \frac{1}{2} \lambda * \sum\|W\|\\)
* __L2:__ \\(L(W) = \lambda * \sum W^2 \\)
* __Elastic net:__  \\(L(W) = \lambda * \sum(βW2 + W) \\)
* __Max norm:__ force \\(\|\|w\|\|\_2 < c \\)
* __Dropout:__ drop random units in previous layers before feeding to the next layer. This technique is specific for neural network.

__Parameter Estimates__

There is usually no closed form solution to minimize the loss function in neural network. Unlike loss function in regression and logistics regression where there is no local minima, neural network's loss function usually has local minima. Therefore, it is possible that if we train neural network mutltiple times, we would obtain different parameter estimates.

We rely on gradient descent to estimate parameters. The gradient is caculated from the output layer and back-propagated to previous layers using chain rule:
\\[
dw_{ij} \equiv \frac{\partial E_n}{\partial w_{ij}^{(L-1)}} = \frac{\partial E_n}{\partial a_i^{(L)}} \frac{\partial a_i^{(L)}}{\partial w_{ij}^{(L-1)}} \\\
\frac{\partial a_i^{(L)}}{\partial w_{ij}^{(L-1)}} = z_j^{(L-1)}
\\]

\\[
\delta_i^{(L)} \equiv \frac{\partial E_n}{\partial a_i^{(L)}} = h'(a_i^{(L)}) \sum_k w_{ik}^{(L+1)} \delta_k^{(L+1)}
\\]

We can update parameter \\(w\\) using direct gradient \\(dw\\), momentum versions, or per-parameter versions of gradient. Direct gradient is sufficient to train simple network. For deep network which requires long training time, momentum versions, or per-parameter versions of gradient are usually used to facilitate faster convergence.
* __Direct gradient:__
\\[
w = w - learningRate * dw
\\]
* __Momentum:__ the parameters will build up velocity in any direction that has consistent gradient
\\[
v = v * \mu - learningRate * dw \\\
w = w + v
\\]
* __Adagrad:__ the parameters that receive high gradients will have their effective learning rate reduced, while parameters that receive small or infrequent updates will have their effective learning rate increased
\\[
cache = cache + dw^2 \\\
w = w - learningRate * dw / (\sqrt{cache} + \epsilon)
\\]
* __RMSprop:__ similar with Adagrad with an attempt to reduce its aggressive, monotonically decreasing learning rate by making cache variable "leaky"
\\[
cache = decay_rate * cache + (1 - decay_rate) * dw^2 \\\
w = w - learningRate * dw / (\sqrt{cache} + \epsilon)
\\]
* __Adam:__ RMSprop with momentum
\\[
m = \beta1 * m + (1-\beta1) * dw \\\
v = \beta2* v + (1-\beta2) * (dw^2) \\\
x = x - learningRate * m / (\sqrt{v} + \epsilon)
\\]
* __Newton’s method:__ requires second order derivatives computation. This approach leads to very fast convergence compared to first-order gradient, but it is too computational expensive for deep network.

Setting a good LearningRate is important for neural network training to converge to a good minimum.
<div class="imgcap">
<div >
    <img src="/blog/assets/neural-network/learning_rate.png" width = "500">
</div>
</div>

## 3. Convolutuional Neural Network
A convolutional Neural Network (ConvNet) has special network architecture that handle matrix inputs such as images. Hidden layers in convolutional architecture usually include a series of Conv-ReLU-Pool layers followed by a number of Fuly-connected layers.
* __Input layer:__ holds the raw pixel values of each input in [MxM] matrix
* Convolution layer (Conv): compute result of performing convolution operation of kernel filter [FxF] on previous layer's [MxM] matrix
<div class="imgcap">
<div >
    <img src="/blog/assets/neural-network/conv.jpg" width = "300">
</div>
</div>
* __Rectified Linear Unit layer (ReLU):__ applies ReLU activation function on each element of result from Convolution layer
* __Pool layer:__ performs a downsampling operation using pooling filter [PxP] along the spatial dimensions. The most commonly used pooling technique is Max-pooling.
Setting a good LearningRate is important for neural network training to converge to a good minimum.
<div class="imgcap">
<div >
    <img src="/blog/assets/neural-network/pool.png" width = "200">
</div>
</div>
* __Fully-connected layer:__ computes the prediction scores. This is a normal hidden layers like those in multi-layer perceptron.
* __Output layer:__ holds value for dependent variable.

<div class="imgcap">
<div >
    <img src="/blog/assets/neural-network/ConvNet.jpg" width = "600">
</div>
</div>

Conv-ReLU-Pool layers are able to extract features from input matrix with increasing complexity. For example, the first Conv layer can extract curves, the second Conv layer can extract shape, the third layer can extract simple objects, etc. Thanks to max-pooling operation, Convolution is translation invariance, i.e. it can detect feature even when such feature is shifed or rotated.

## 4. Recurrent Neural Network
A recurrent neural network (RNN) is a special neural network where connections between units form a directed cycle, enabling the network to handle inputs with temporal behavior such as word sequence in a sentence. RNN has many variants, each exhibiting different temporal relationsips.
* __Recursive Neural Network:__ tree-like structure, useful in representing nested realtionship (eg. a sentence comprises of sequence of phrases, which are made of sequence of words).
<div class="imgcap">
<div >
    <img src="/blog/assets/neural-network/recursive.png" width = "600">
</div>
</div>

* __Fully-Recurrent Network:__ the most commonly used architecture for RNN, simply representing sequence of data (eg. a sentence comprises of sequence of words).
<div class="imgcap">
<div >
    <img src="/blog/assets/neural-network/rnn.png" width = "600">
</div>
</div>

Basic RNN only comprises of simple units with sigmoid or tanh activation function and usually handles long-term dependency poorly. In practice, more complicated units are used:
* __Long-Short Term Memory (LSTM):__
<div class="imgcap">
<div >
    <img src="/blog/assets/neural-network/lstm.png" width = "200">
</div>
</div>
* __Gated Recurrent Unit (GRU):__
<div class="imgcap">
<div >
    <img src="/blog/assets/neural-network/gru.png" width = "200">
</div>
</div>
LSTM and GRU both have three similar sigmoid gates to control what information to forget, what new information to retain and what information to output.

While a convolutional neural network specializes in handling spatial feature, a recurrent neural network can use its internal memory in recurrent hidden units to process temporal feature. It is not uncommon to combine convolutional neural network and recurrent neural network to handle inputs involving both image data and sequential data such as video.
