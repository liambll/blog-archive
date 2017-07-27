---
layout: post
comments: true
title:  "Probabilistic Graphical Model"
title2:  "Probabilistic Graphical Model"
date:   2017-07-26 17:22:00
permalink: /graphical-model/
mathjax: true
tags: Machine-Learning Probabilistic-Graphical-Model bayesian-statistics statistics
categories: Machine-Learning Statistics
img: /blog/assets/graphical-model/graphical-model.png
summary: A probabilistic graphical model (PGM) is a probabilistic model for which a graph expresses the conditional dependence structure between random variables...
---


"A probabilistic graphical model (PGM) is a probabilistic model that uses a graph to express the conditional dependence structure between random variables." Probabilistic graphical model is a marriage of Bayesian statistics and machine learning.

## 1. Description
Probabilistic graphical models use a graph-based representation of a set of independences among random variables. There two common branches of graphical models:
* Directed graphical model, or Bayesian Network: represents a set of random variables and their conditional dependencies using a directed acyclic graph:
<div class="imgcap">
<div >
    <img src="/blog/assets/graphical-model/bayesian-network.png" width = "300">
</div>
</div>

* Undirected graphical model, or Markov Random Field: represents a set of random variables and their conditional dependencies using an undirected graph, which can be acyclic or cyclic.
<div class="imgcap">
<div >
    <img src="/blog/assets/graphical-model/markov-random-field.png" width = "300">
</div>
</div>

TBC
