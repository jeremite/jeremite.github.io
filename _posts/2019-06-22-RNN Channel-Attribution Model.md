---
layout: post
title:  "Attention-RNN Channel-Attribution Model"
date:   2019-06-22
excerpt: "An integrated Neural Network for Sequential Channel Path and Customer Profile Data"
project: true
tag:
- Attention Mechanism 
- LSTM, RNN
- Embedding Layer
- Multi-Channel Attribution
comments: true
---

CLICK HERE:
[Full Python Code](https://github.com/jeremite/channel-attribution-model/blob/master/FFDNA.py)

CLICK HERE:
[Full Medium Blog](https://medium.com/@wli10/how-to-implement-an-attention-rnn-into-solving-the-multi-channel-attribution-problem-6fa90d935859)


## Overview
In this project, I present a novel unified framework for marketing budget allocation on different customer digital channels, which contains two sequential steps: learning cusotmer conversion (purchase or not) models from historical data, and optimizing budget allocation based on learned models. The whole framework is illustrated as follows:

![Model Architecture](https://github.com/jeremite/jeremite.github.io/blob/master/assets/img/Post/attribution1.png?raw=true) 


## Challengs
1. The data are either having sequential pattern or non-sequential pattern, so the model couldn't be solely Recurrent Neural Network or plain Deep Neural Network.
2. The non-sequential data can be further divided into continuous and discrete data.
3. There are several gaps between Neural Nets and Decision Making. One of the biggest challenges is that it is too difficult to 
translate black-box forecasting into allocation decisions.

## Solutions
1. Build a unified framework that combines Recurrent Neural Net and plain Deep Neural Net. The former one can capture the sequential pattern of the customer path data (comprised of digital channels), while the latter one deals with non-sequential customer profile data.
2. For the non-sequential customer data, construct an Embedding Layer for the discrete part.
3. Add an Attention Layer used to allocate weights to different channels along the customer journey.

## Details
Since I've already written an article about it on Medium.com, **please check it out through the link above.**
The business problem is as follows:

![business problem](https://github.com/jeremite/jeremite.github.io/blob/master/assets/img/Post/attribution2.png?raw=true) 

The raw data is like this (I need to collapse the channel column into sequence-like path data):

![raw data](https://github.com/jeremite/jeremite.github.io/blob/master/assets/img/Post/attribution3.png?raw=true) 


