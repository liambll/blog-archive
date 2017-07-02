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
summary: Queuing model is a mathematical model that predict queue lengths and waiting time...
---


"Queuing model is a mathematical model that predict queue lengths and waiting time" to help business decide actions to take in order to keep waiting time or queue length at desired level.

## 1. Model
<div class="imgcap">
<div >
    <img src="/blog/assets/queuing-model/queuing-model.jpg" width = "500">
</div>
</div>
__* Arrivals:__
  * The time between consecutive arrivals to a queueing system is the interarrival time.
  * Mean arrival rate \\(\lambda\\) is the expected number of arrivals per unit time.
\\[
{\text{Expected interarrival time}} = 1/\lambda
\\]
  * Most queueing models assume that the form of the probability distribution of inter‐arrival times is an exponential distribution. That means the probability of an arrival in the next time unit is completely uninfluenced by when the last arrival occurs (i.e. lack-of-memory property) and there is a high likelihood g of small interarrival times, and a small chance of a very large interarrival time.

__* Queue:__
  * The number of customers in the queue \\(L_q\\) is the number of customers waiting for service to begin.
  * The number of customers in the system \\(L\\) is the number in the queue plus the number currently being served.
  * The queue capacity is the maximum number of customers that can be held in the queue.
  * The queue discipline refers to the order in which members of the queue are selected to begin service. Examples include First-In-First Out (FIFO), random selection, priority procedure, and even Last-In-First-Out (LIFO)

__* Service:__
  * Service time is the elapsed time from the begining to the end of service.
  * Mean service rate \\(\mu\\) is expected number of service completions per unit time for a single busy server
\\[
{\text{Expected service time}} = 1/\mu
\\]
  * Most queueing models assume that the service time has a particular probability distribution, such as exponential distribution, constant-time service time, etc.
  * Number of servers \\(s\\)
  * Utilization factor \\(ρ\\) is the average fraction of time that a server is busy serving customers
\\[
ρ = \lambda /s\mu
\\]

Queuing models are usually labeled in the form:
\\[
{\text{Interarrival time distribution / Service time distribution / No. Servers}}
\\]
  * \\(M\\): Exponential distribution (Markovian)
  * \\(D\\): Degenerate distribution (constant times)
  * \\(GI\\): General independent interarrival‐time distribution (any distribution)
  * \\(G\\): General service‐time distribution (any distribution)

For example, M/M/s denotes a queuing model with multiple servers and exponential distribution for interarrival time and service time.

## 2. Estimation
Queuing models can provide estimations for:
  * \\(L\\) = Expected number of customers in the system, including those being served (Line Length).
  * \\(L_q\\) = Expected number of customers in the queue, which excludes customers being served.
  * \\(W\\) = Expected waiting time in the system (including service time) for an individual customer
  * \\(W_q\\) = Expected waiting time in the queue (excludes service time) for an individual customer.

__Little's Formula:__
\\[
L = \lambda W
\\]
\\[
L_q = \lambda W_q
\\]
\\[
W = W_q + 1/\mu
\\]
\\[
L = L_q + \lambda /\mu
\\]
Below are mathematical solution to several simple queuing models.

__* M/M/1 Model:__

M/M/1 denotes a queuing model with single server and exponential distribution for interarrival time and service time.
\\[
L_q = ρ^2(1-ρ) = \lambda ^2/[\mu (\mu - \lambda)]
\\]
\\[
L = ρ(1-ρ) = \lambda /(\mu - \lambda)
\\]
\\[
W_q = \lambda /[\mu (\mu - \lambda)]
\\]
\\[
W = 1 /(\mu - \lambda)
\\]
Probability of having exactly n customers in the system:
\\[
P(L=n) = ρ(1-ρ)
\\]
Probability of waiting time in the system exceeding t:
\\[
P(W > t) = exp(-\mu(1-ρ)t)
\\]
Probability of waiting time in the queue exceeding t:
\\[
P(W_q > t) = ρexp(-\mu(1-ρ)t)
\\]


__* M/G/1 Model:__

M/G/1 denotes a queuing model with single server, exponential distribution for interarrival time and general distribution for service time, which has mean \\(1/\mu\\) and standard deviation \\(\sigma\\).
\\[
L_q = (\lambda^2 \sigma^2 + ρ^2)/(2(1-ρ))
\\]


__* M/D/1 Model:__

This is a special case of M/G/1 model with \\(\sigma\\) = 0.
\\[
L_q = ρ^2/(2(1-ρ))
\\]
We can clearly see the impact of service variability on the system performance: Changing from the exponential service time to the one
that has no variability has a dramatic impact on reducing waiting time and queue length.


