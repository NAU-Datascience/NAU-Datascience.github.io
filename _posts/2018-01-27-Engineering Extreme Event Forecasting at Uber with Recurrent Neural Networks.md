---
layout: post
current: post
<!-- cover:  assets/images/welcome.jpg -->
navigation: True
title: Engineering Extreme Event Forecasting at Uber with Recurrent Neural Networks
date: 2018-01-29 23:05:00
tags: [Summary, Data Science, Anomaly]
class: post-template
subclass: 'post tag-getting-started'
author: hamza

---



### *By Nikolay Laptev, Slawek Smyl, & Santhosh Shanmugam*

[Link to full post](https://eng.uber.com/neural-networks/)

The goal of the experiment is predicted where, when, and how many rides requests Uber will receive at any given time. Creating this model is challenging because for special days in the year, there are numerous unexpected activities. For example, NYE (new years eve) is a very busy day for uber, but it is not correlated with the month or anything also this kind of days happens once in a year so hard to get in data. In addition to historical data, extreme event prediction also depends on numerous external factors, including weather, population growth etc.

![](http://eng.uber.com/wp-content/uploads/2017/06/image2-2.png)

## Creating Uber’s new extreme event forecasting model

They decided to use LSTD and because of data shortages, they use data from many cities at once, which greatly improved our accuracy.

## Building a new architecture with neural networks

This raw data was used in our training model to conduct simple preprocessing, including log transformation, scaling, and data detrending.

### Training with sliding windows



![](http://eng.uber.com/wp-content/uploads/2017/06/image2-e1496957521819.png)



### Tailoring our LSTM model 

During testing, vanilla (the not customized form of) LSTM did not perform superior performance compared to the baseline model, which included a combination of univariate forecasting and machine learning elements.

To improve our accuracy, they incorporated an automatic feature extraction module into our model, depicted below:

![](http://eng.uber.com/wp-content/uploads/2017/06/Screen-Shot-2017-06-08-at-2.33.18-PM-e1496957645776.png)



the model first primes the network by automatic, ensemble-based (combining multiple models) feature extraction. After feature vectors are extracted, they are averaged using a standard ensemble technique. The final vector is then concatenated with the input to produce the final forecast.

During testing, they were able to achieve a 14.09 percent symmetric mean absolute percentage error (SMAPE) improvement over the base LSTM architecture.

## Using the new forecasting model

For the purpose of this article, they built a model using the five-year daily history of completed Uber trips across the U.S. over the course of seven days before, during, and after major holidays like Christmas Day and New Year’s Day.

![](http://eng.uber.com/wp-content/uploads/2017/06/Screen-Shot-2017-06-08-at-2.45.13-PM.png)

![](http://eng.uber.com/wp-content/uploads/2017/06/image3-1.png)



From our experience, they define three dimensions for deciding if the neural network model is right for your use case: (a) number of time series, (b) length of time series, and (c) correlation among time series. All three of these dimensions increase the likelihood that the neural network approach will forecast more accurately relative to the classical time series model.

### Forecasting in the Future

If this type of research excites you (and you happen to be Down Under, check out Uber’s time series workshop during the International Machine Learning Convention on August 6, 2017, in Sydney.
