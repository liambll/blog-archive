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
* Directed graphical model, or Bayesian Network: represents a set of random variables and their conditional dependencies using a directed acyclic graph. For example, a Bayesian Network can represents the relationship between diseases, symptoms and treatment. There are induced dependencies in Bayesian Network, eg. diseases cause certain symptoms, diseases and symptoms lead to certain treatment.
<div class="imgcap">
<div >
    <img src="/blog/assets/graphical-model/bayesian-network.png" width = "300">
</div>
</div>

__Joint-probability distribution:__ product of conditional probabilities of each node \\(i\\) given its acenstors \\(A_i\\).
\\[
p(x_1,x_2,..,x_k) = \prod p(x_i|x_A_i)
\\]
In the above example, we have \\(p(A,B,C,D,E,F) = p(A) p(B|A) p(C|A,E) p(D|B) p(E|B) p(F|C,D,E) \\)

__Conditional Dependencies:__ In a Bayesian Network \\(X,Y|Z\\) if \\(X\\) and \\(Y\\) are __[d-seperated](https://en.wikipedia.org/wiki/Bayesian_network#d-separation)__ given \\(Z\\).

* Undirected graphical model, or Markov Network, Markov Random Field: represents a set of random variables and their conditional dependencies using an undirected graph, which can be acyclic or cyclic. Depedencies in Markov Network are not induced. For example, Markov Network can represent an image, with each pixel is one node in the graph. We cannot say a pixel would affect pixels surrouding it, but we can say pixels belong to the same objects might be related to each other.
<div class="imgcap">
<div >
    <img src="/blog/assets/graphical-model/markov-random-field.png" width = "300">
</div>
</div>

__Joint-probability distribution:__ product of score function of each [clique](https://en.wikipedia.org/wiki/Clique_(graph_theory)) \\(c\\), normalized by a constant \\(Z\\) to push the value to 1.
\\[
p(x_1,x_2,..,x_k) = \frac{1}{Z} \prod \theta_i(c_i) \\\
Z = \sum \prod \theta_i(c_i)
\\]
In the above example, we have \\(p(A,B,C,D,E,F) = \frac{1}{Z} \theta(A,B,D) \theta(D,E) \theta(C,E) \\)

__Conditional Dependencies:__ In a Markov Network, \\(X,Y|Z\\) if \\(X\\) and \\(Y\\) are not connected by a path if \\(Z\\) is observed. A __Markov blanket__ \\(U\\) of a variable \\(X\\) is the minimal set of nodes such that \\(X\\) is independent from the rest of the graph if \\(U\\) is observed.

A Bayesian Network can always be converted to a Markov Network through a process called _moralization_, i.e. adding side edges to all parents of a node and removing their directionality. Markov Networks are more general and plexible, but are more difficult to deal with computationally compared to Bayesian Networks.

There are other specialized probabilistic graphical models (factor graph, restricted Boltzmann machine, etc), but these models will not be discussed here.

## 2. Mathematics
TBC

