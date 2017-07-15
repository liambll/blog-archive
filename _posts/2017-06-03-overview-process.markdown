---
layout: post
comments: true
title:  "Analytic Process Overview"
title2:  "Analytic Process Overview"
date:   2017-06-03 15:22:00
permalink: /overview-process/
mathjax: true
tags: Overview
categories: Overview
img: /blog/assets/overview/overview.png
summary: Data analytics techniques generally fall in to one of three non mutually exclusive fields...
---

Data analytics process (also known as data science pipeline) describes recommended tasks to perform in order to extract insight from data. A best practice data analytics process proposed by the Institute for Operations Research and Management Sciences (INFORMS) is shown below:

<div class="imgcap">
<div >
    <img src="/blog/assets/overview/Analytics-Process.png" width = "700">
</div>
</div>

## 1. Business Problem Framing
It is important to obtain a clear objective at this initial stage. The key is to be specific (5W is useful here).
* understand business problem, its benefits and constraints
* determine if the business problem can potentially be solved with an analytics solution

For example, "sales performance" can refer to total sales, sales margin, sales per customer, etc. In this specific scenario, we want to increase sales per customer. There are several analytics approaches we can employ. For example, based on historical purchases, we can attempt to perform individual price optimization (Opertions Research technique). We can also conduct experiments to find out factors influencing purchasing decision and change those factors to drive customer purchases (Statistical Analysis technique). We can even send recommendation to each customer about products that similar people have bought in the past (Machine Learning technique).

## 2. Analytics Problem Framing
This step is the "last chance to correct any mistakes or misunderstanding while it is still cheap to do so".
* reformulate business problem into an analytics problem with initial set of drivers (inputs, outputs)
* specify assumptions and success metrics

Let's say we want to find out factors influencing purchasing decision and change those factors to drive customer purchases. We assume that increasing number of purchases would increase sales per customer. Initial set of inputs would be price, product feature, location, promotion, customer demographics factors. Ouput would be purchase decision, i.e. whether a customer bought a product. We also need to narrow down the success metrics: Are we going to measures sales per customer across the whole company, in a specific geographcial area, or in a specific customer group? These metrics would influence what data we need to collect and analyze.


## 3. Data Collection
This is probably the most boring and time consuming step, but it is crucial to have quality data before proceeding to model building.
* identify data sources and acquisition
  * identify data points: sampling method, experiment design
  * determine sample size
  * determine variables and possible values
  * determine control group (if applicable)
* perform data exploration and preprocessing
  * univariabte analysis
  * bivariable analysis
  * missing value treatment: deletion, imputation, random imputation
  * outlier detection (Box Plot, Histogram, Scatter Plot) and treatment (deletion, transformation, separate treatment)
  * feature extraction: normalization and standardization, dimentionality reduction, fourier transform, format conversion
  
## 4. Model Building
Depending on the nature of the analytics problem, it might be neccesary to compromise model accuracy to gain model intepretability.
* identify available quantitative methods for the analytics problem
* perform model building and evaluation. Variable selection in model building include filter method, wrapper method, embedded method. Common evaluation criteria are:
  * continious output variable: sum of square error
  * ordinal output variable: concordance, discordance, ROC/c-statistics
  * binary output variable: accuracy, precision, recall, f-score

There are many models that can predict binary outcome (purchase decision) based on a set of explanatory variables: logistics regression, support vector machine, neural network, etc. If it is imporant to explain how each explanatory variable influence purchasing decision, we would choose logistics regression even though it has lower accuracy comapred to support vector machine and neural network.

## 5. Model Deployment
* perform business validation of the selected model
* integrate model in existing process in production environment
* monitor business performance and recalibrate the model

Regardless of how high the model's accuracy is, it needs to actually increase sales per customer. That is why we always need to perform business validation of the selected model. For example, we can carry out an A/B testing to compare sales per customers between using the model vs. not using the model. A model with high accuracy might turn out to increase little sales per customer. That means some of the assumptions are not valid (most likely), or data quality is questionable, or the model and evaluation criteria are not suitable. 

Monitoring business performance overtime can help detect changes that might invalidate previous model assumptions, and provide a mean to measure values brought by the model.
