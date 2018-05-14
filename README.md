## Introduction
In this repo, we will try to re-implement the algorithm discussed in this [paper](https://arxiv.org/pdf/1804.07931.pdf) authored by Alibaba engineering group, with focus on estimating post-click conversion activity.

In general, the sequential order of user actions in response to an online ads is, impression -> click -> conversion. The click and conversion are both rare events in comparison to their base events. Given the specific program, the main challenges to model CvR (conversion rate, #conversion / #click) can be summarized in following points:
    * sample selection bias: traditionally, pCvR model is trained with clicked impression data, while being utilized to estimate all impressions. Clicked impression is only a small fraction of total impression events (normally: 1% - 5%).
    * data sparsity: conversion events can take place only after click events happen at rate of ~1%. Therefore, conversion events are very sparse.
    * time delay: conversion event can happen from seconds after events to few days/weeks after any engagement (etc. impression, clicks) with ads.

### Candidate Model Architects 
