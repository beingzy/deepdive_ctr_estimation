## Introduction
In this repo, we will try to re-implement the algorithm discussed in this [paper](https://arxiv.org/pdf/1804.07931.pdf) authored by Alibaba engineering group, with focus on estimating post-click conversion activity.

In general, the sequential order of user actions in response to an online ads is, impression -> click -> conversion. And, their probabilities can be formulated as below:

$$
p(conversion=1, click=1|impression) = p(click=1|impression) * p(conversion=1|click=1, impression)
$$

The click and conversion are both rare events in comparison to their base events. Given the specific program, the main challenges to model CvR (conversion rate, #conversion / #click) can be summarized in following points:

    * sample selection bias: traditionally, pCvR model is trained with clicked impression data, while being utilized to estimate all impressions. Clicked impression is only a small fraction of total impression events (normally: 1% - 5%).
    * data sparsity: conversion events can take place only after click events happen at rate of ~1%. Therefore, conversion events are very sparse.
    * time delay: conversion event can happen from seconds after events to few days/weeks after any engagement (etc. impression, clicks) with ads.

### Candidate Model Architects
In this paper, it introduced a ESMM architect to train for two events, click and conversion, simultaneously, to mitigate the issues of training post-impression conversion model. Training for click alongside conversion events at same time and share embedding layers which learned from clicked impressions with conversion model to mitigate the data sparsity issue.
By training with all impression data, it reduce the sample selection bias issue.

High level characteristics of the neural networks:
    1) ReLU activation function is used;
    2) dimension of embedding vector is set to be 18;
    3) demension of each layers in MLP are: 360 * 200 * 80 * 2
    4) adam solver is used with initial parameters: $\beta_1 = 0.9$, $\beta_2 = 0.999$, $\epsilon=10^{-8}$


### Reference Worth Mentioning
    * [Modeling Delayed Feedback in Display Advertising](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.650.6087&rep=rep1&type=pdf)
    * [An Overview of Multi-Task Learning in Deep Neural Networks](https://arxiv.org/abs/1706.05098)
    * [Mining with Rarity: a Unifying Framework](https://dl.acm.org/citation.cfm?id=1007734)
    * [Handling class imbalance in customer churn prediction](https://www.sciencedirect.com/science/article/pii/S0957417408002121)
