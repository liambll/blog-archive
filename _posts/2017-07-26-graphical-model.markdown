---
layout: post
comments: true
title:  "Probabilistic Graphical Model"
title2:  "Probabilistic Graphical Model"
date:   2017-07-26 17:22:00
permalink: /graphical-model/
mathjax: true
tags: Machine-Learning Probabilistic-Graphical-Model Bayesian-Statistics Statistics
categories: Machine-Learning Statistics
img: /blog/assets/graphical-model/graphical-model.png
summary: A probabilistic graphical model (PGM) is a probabilistic model for which a graph expresses the conditional dependence structure between random variables...
---


"A probabilistic graphical model (PGM) is a probabilistic model that uses a graph to express the conditional dependence structure between random variables." Probabilistic graphical model is a marriage of Bayesian Statistics and Machine Learning. Applications of graphical models include causal inference, speech recognition, image restoration, diagnosis of diseases.

## 1. Description
Probabilistic graphical models use a graph-based representation of a set of independences among random variables. There two general branches of graphical models:
* __Directed graphical model__, or __Bayesian Network__: represents a set of random variables and their conditional dependencies using a directed acyclic graph. For example, a Bayesian Network can represents the relationship between diseases, symptoms and treatment. There are induced dependencies in Bayesian Network, eg. diseases cause certain symptoms, diseases and symptoms lead to certain treatment.
<div class="imgcap">
<div >
    <img src="/blog/assets/graphical-model/bayesian-network.png" width = "300">
</div>
</div>

__Joint-probability distribution:__ product of conditional probabilities of each node \\(i\\) given its acenstors \\(A_i\\).
\\[
p(x_1,x_2,...,x_k) = \prod_i p(x_i\|x_{A_i})
\\]
In the above example, we have
\\(p(A,B,C,D,E,F) = p(A) p(B\|A) p(C\|A,E) p(D\|B) p(E\|B) p(F\|C,D,E) \\).

__Conditional Dependencies:__ In a Bayesian Network \\(X,Y\|Z\\) if \\(X\\) and \\(Y\\) are __[d-seperated](https://en.wikipedia.org/wiki/Bayesian_network#d-separation)__ given \\(Z\\).

* __Undirected graphical model__, or __Markov Network__, __Markov Random Field__: represents a set of random variables and their conditional dependencies using an undirected graph, which can be acyclic or cyclic. Depedencies in Markov Network are not induced. For example, Markov Network can represent an image, with each pixel is one node in the graph. We cannot say a pixel would affect pixels surrouding it, but we can say pixels belong to the same objects might be related to each other.
<div class="imgcap">
<div >
    <img src="/blog/assets/graphical-model/markov-random-field.png" width = "300">
</div>
</div>

__Joint-probability distribution:__ product of potential function \\(\phi\\) of each [clique](https://en.wikipedia.org/wiki/Clique_(graph_theory)) \\(c\\), normalized by a constant \\(Z\\) to push the sum of probabilities to 1.
\\[
p(x_1,x_2,..,x_k) = \frac{1}{Z} \prod_c \phi_c(x_c) \\\
Z = \sum \prod_c \phi_c(x_c)
\\]
In the above example, we have \\(p(A,B,C,D,E,F) = \frac{1}{Z} \phi(A,B,D) \phi(D,E) \phi(C,E) \\).

__Conditional Dependencies:__ In a Markov Network, \\(X,Y\|Z\\) if \\(X\\) and \\(Y\\) are not connected by a path if \\(Z\\) is observed. A __Markov blanket__ \\(U\\) of a variable \\(X\\) is the minimal set of nodes such that \\(X\\) is independent from the rest of the graph if \\(U\\) is observed.

A Bayesian Network can always be converted to a Markov Network through a process called _moralization_, i.e. adding side edges to all parents of a node and removing their directionality. Markov Networks are more general and plexible, but are more difficult to deal with computationally compared to Bayesian Networks.

When a Markov Random Field is used to model conditional probability \\(p(y\|x)\\), it is called a __Conditional Random Field__.
\\[
p(y\|x) = \frac{1}{Z(x)} \prod_c \phi_c(x_c, y_c) \\\
Z = \sum_y \prod_c \phi_c(x_c, y_c)
\\]

There are other specialized probabilistic graphical models (factor graph, restricted Boltzmann machine, etc), but these models will not be discussed here.

## 2. Mathematics
There are several tasks we usually perform in probabilistics graphical model:
* __Inference:__ Given a probabilistic model, we can ask:
  * Marginal Inference: what is the probability of a given variable?
  * Maximum a posteriori (MAP) inference: what is the most likely assignment to the variables in the model, conditioned on data?
* __Learning:__ Given a dataset, we would like to fit the best model:
  * Parameter Learning: estimate the parameters in the graph, i.e. what is the most likely assignment to parameters in the model.
  * Structure Learning: estimate the structure of the graph, i.e. determine from data how the variables depend on each other.

Exact inference methods include:
* __Variable Elimination:__ The variable elimination method repeatedly perform two factor operations: product and marginalization in order to perform marginal inference for a specific variable:
  * Product operation: \\(\phi_3(x_c) = \phi_1(x_c) \phi_2(x_c) \\)
  * Marginalize operation: \\(\tau(x) = \sum_y \phi(x, y) \\)
Variable elimination ordering is important to achieve improvement running time. 

* __Belief Propagation:__ Belief Propagation method stores intermediate \\(\tau\\) values while performing variable elimination for the first time. After that, when we need to perform marginal inference for another variable, we can immidiately caculate the result using belief propagation without running variable elimination algorithm again.

* __MAP inference:__

The probabilistic models are often quite complex, and exact inference may be too slow for them. Approximation solutions include:
* __Sampling method:__ produce answers by repeatedly generating random numbers from distributions in the model. Sampling from distributions can help perform many tasks, including marginal and MAP inference, as well as estimating integrals:
\\[
E_{x~p}[f(x)] = \sum_x f(x)p(x)
\\]
  * Rejection sampling: compute the area of a region \\(R\\) by sampling in a larger region with a known area and recording the fraction of samples that falls within \\(R\\).
  * Importance sampling: sample from an alternative distribution q, and then reweigh the samples in a way that their sum still approximates the desired integral for p.
  * Markov Chain Monte Carlo method: sample from distributions sequentially: Metropolis-Hastings algorithm, Gibbs sampling.

* __Variational method:__ cast inference as an optimization problem by choose an approximating distribution family \\(Q\\) and minizming Kullback-Leibler divergence between \\(Q\\) and actual distribution \\(P\\). In information theory, KL divergence is used to measure differences in information contained within two distributions.
\\[
KL(q\|\|p) = \sum_x q(x)\log\fract{q(x)}{p(x)}
\\]
There are many proposal for approximating distribution family \\(Q\\): exponential families, neural networks, Gaussian processes, latent variable models, etc. One of the most widely used classes of distributions is simply the set of fully-factored \\(q(x)\\), and such variational inference is called __Mean-field inference__.
\\[
q(x) = q_1(x_1)q_2(x_2)...q_n(x_n)
\\]


