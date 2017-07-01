---
layout: post
comments: true
title:  "Queuing Model"
title2:  "Queuing Model"
date:   2017-07-02 16:22:00
permalink: /queuing-model/
mathjax: true
tags: Operations-Research Queuing-Model
categories: Operations-Research
img: /blog/assets/queuing-model/queuing-model.jpg
summary: Queueing model is a mathematical model that predict queue lengths and waiting time...
---


"Queueing model is a mathematical model that predict queue lengths and waiting time."


## 1. Model
<div class="imgcap">
<div >
    <img src="/blog/assets/queuing-model/queuing-model.jpg" width = "500">
</div>
</div>
* Arrivals:
  * The time between consecutive arrivals to a queueing system is the interarrival time.
  * Mean arrival rate \lambda is the expected number of arrivals per unit time.
\[ Expected interarrival time = 1/\lambda \]
Most queueing models assume that the form of the probability distribution of inter‐arrival times is an exponential distribution. That means the probability of an arrival in the next time unit is completely uninfluenced by when the last arrival occurs (i.e. lack-of-memory property) and there is a high likelihood g of small interarrival times, and a small chance of a very large interarrival time.
* Queue:
  * The number of customers in the queue (L_{\text{q}}) is the number of customers waiting for service to begin.
  * The number of customers in the system (L) is the number in the queue plus the number currently being served.
  * The queue capacity is the maximum number of customers that can be held in the queue.
  * The queue discipline refers to the order in which members of the queue are selected to begin service. Examples include First-In-First Out (FIFO), random selection, priority procedure, and even Last-In-First-Out (LIFO)
* Service:
  * Service time is the elapsed time from the begining to the end of service.
  * Mean service rate \mu is expected number of service completions per unit time for a single busy server
\[ Expected service time = 1/\mu \]
Most queueing models assume that the service time has a particular probability distribution, such as exponential distribution, constant-time service time, etc.


