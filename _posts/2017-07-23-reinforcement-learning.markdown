---
layout: post
comments: true
title:  "Reinforcement Learning"
title2:  "Reinforcement Learning"
date:   2017-07-23 17:22:00
permalink: /reinforcement-learning/
mathjax: true
tags: Machine-Learning Reinforcement-Learning
categories: Machine-Learning
img: /blog/assets/reinforcement-learning/reinforcement-learning.png
summary: Reinforcement learning is a machine learning area that seek to learn how software agents should take actions in an environment in order to maximize some notion of cumulative reward...
---


"Reinforcement learning is a machine learning area that seek to learn how software agents should take actions in an environment in order to maximize some notion of cumulative reward."
* Compared to Supervised Learning: If we treat a supervised learning problem as a decision making problem, agent's action is predition value, and we can immidiately see the reward, which is accuracy of the prediction. In reinforcement learning, we do not know the reward until the agent performs multiple actions. Immitation learning is something in between supervised learning and reinforcement learning, in which input data contains different actions and output is whether such action is good or bad.
* Compared to Decision Analysis in Operations Research. In Operations Research, decision analysis is usually conducted assuming actions don't change state of the environment. On the other hand, in reinforcement learning, the agent's actions change state of the environment.

## 1. Description
Reinforcement learning model for an agent in an environment can be described using Markov Decision Process \\(<S,A,R,T,\gamma>\\). It assumes Markov property, i.e. outcome of an action depends only on the current state and not previous states: \\(p(s_{1+1}|s_1,a_1,...s_t,a_t) = (p(s_{1+1}|s_t,a_t) \\).
* __Action:__ a set \\(A\\) of actions that the agent can perform
* __State:__ a set \\(S\\) of the environment states
* __T:__ a temporal model specifying state \\(s_{t+1}\\) achieved when the agent perform action \\(a_t\\) on environment state \\(s_t\\)
* __Reward:__ a reward model \\(R(s)\\), \\(R(s,a)\\), or \\(R(s,a,s')\\) specifying reward \\(r_t\\) achieved when the agent perform action \\(a_t\\) on environment state \\(s_t\\)
* __Discount factor:__ since we only know the final reward at the end, discount factor \\(\gamma \lte 1\\) is used to measure reward \\(R(s_t)\\) at time t based on final reward.

<div class="imgcap">
<div >
    <img src="/blog/assets/reinforcement-learning/reinforcement-learning.png" width = "500">
</div>
</div>

## 2. Mathematics
We want to find __Policy \\(\pi\\): S -> A__ that specifies optimal action to take in each state.

Given state \\(s\\), __Value of policy \\(V^\pi(s)\\)__ is the expected discounted sum of rewards obtain if we follow policy \\(\pi\\) starting with state s until the end.
\\[
V^\pi(s) = \sum_{i=0}^∞ \gamma^i r(s_i, \pi(s_i)) | s_0 = s
\\]


TBC...
