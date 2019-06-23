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

Since I've already written an article about it, please check it out through the link above.

## Overview
In this project, I present a novel unified framework for marketing budget allocation on different customer digital channels, which contains two sequential steps: learning cusotmer conversion (purchase or not) models from historical data, and optimizing budget allocation based on learned models. The whole framework is illustrated as follows:

## Challengs
1. The data are either having sequential pattern or non-sequential pattern, so the model couldn't be solely Recurrent Neural Network or plain Deep Neural Network.
2. The non-sequential data can be further divided into continuous and discrete data.
3. There are several gaps between Neural Nets and Decision Making. One of the biggest challenges is that it is too difficult to 
translate black-box forecasting into allocation decisions.
