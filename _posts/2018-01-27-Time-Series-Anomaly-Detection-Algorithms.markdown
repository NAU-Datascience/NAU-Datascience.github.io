---
layout: post
current: post
<!-- cover:  assets/images/welcome.jpg -->
navigation: True
title: Time Series Anomaly Detection Algorithms
date: 2018-01-27 17:49:00
tags: [Blog Summary, Summary, Data Science, Machine Learning]
class: post-template
subclass: 'post tag-data-science'
author: bedir
---

# Time Series Anomaly Detection Algorithms, Blog Summary

​	_This is a summary of a blog post, published on medium.com._

**Original Blog Post:** [Pavel Tiunov - Jun 8, 2017](https://blog.statsbot.co/time-series-anomaly-detection-algorithms-1cef5519aef2?lipi=urn%3Ali%3Apage%3Ad_flagship3_messaging%3BUw%2FGWSJaTCysr0hAzNNPbw%3D%3D)

## Important Types of Anomalies

Anomaly detection problem for time series is usually formulated as finding outlier data points relative to some standard or usual signal. Some types of anomalies:

- Additive Outliers
- Temporal Changes
- Level shifts or seasonal level shifts

An anamoly detection algorithm should either label each time point as anomaly/not anomaly, or forecast a signal for some point and test if this point value varies from the forecasted enough to deem it as an anomaly.

Using the second approach, you would be able to visualize a confidence interval, which will help a lot in understanding why an anomaly occurs and validate it.

## STL Decomposition

- STL (Seasonal Trend Decomposition based on Loess).
- Gives you ability to split your time series signal into three parts: **Seasonal, Trend, Residue**
- Suitable for seasonal time series, which is the most popular case

**If you analyze deviation of residue and itroduce some threshold for it, you'll get an anomaly detection algorithm**

- You should use **median absolute deviation** to get a more robust detection of anomalies
- Twitter Anomaly detection library ([AnomalyDetection](https://github.com/twitter/AnomalyDetection)) 

### Pros

- Simplicity
- Robust
- Can handle a lot of different situations
- All anomalies can still be intuitively interpreted
- Good for detecting **Additive outliers**
- To detect level changes you can use rolling average signal instead of the original one

### Cons

- Rigidity regarding tweaking options. All you can tweak is your confidence interval using the significance level
- It doesn't work well when characteristics of your signal have changed dramatically

## Classification and Regression Trees

### Supervised Learning

- To teach trees to classify anomaly/non-anomaly data points.
- You need to have **labeled** anomaly data points.

### Unsupervised Learning

- To teach CART to predict next data point in your series and have some confidence interval or prediction error as in the case of STL decomposition.
- Check if data points lie inside or outside of the confidence interval. (Generalized ESD test, or Grubbs' test)

Most popular implementation  to perform learning for trees is the **xgboost** library.

### Pros

- It is not bound in any sense, to the structre of the signal
- You can introduce many feature parameters

### Cons

- Growing number of features can start to impact your computational performance fairly quickly. (Choose your features carefully)

## ARIMA

It’s based on an approach that several points from the past generate a forecast of the next point with the addition of some random variable, which is usually **white noise**. As you can imagine, forecasted points in the future will generate new points and so on. Its obvious effect on the forecast horizon: **the signal gets smoother.**

The difficult part in appliance of this method is that you should [select](https://en.wikipedia.org/wiki/Box%E2%80%93Jenkins_method) the number of **differences**, number of **autoregressions**, and **forecast error coefficients**.

​	_PS: Each time you work with a new signal you should build a new ARIMA model._

- Your signal shouldn't be dependent on the time.

Anomaly detection is done by creating an adjusted model of a signal by using outlier points and checking if it is a better fit than original model by using **t-statistics**.![img](https://cdn-images-1.medium.com/max/1600/0*ObqneGx8Dcla8biC.)

*Two time series built using original ARIMA model and adjusted for outliers ARIMA model.*

- Use tsoutliers (R Package). It is suitable to detect all types of anomalies in the case that you can find a suitable ARIMA model for your signal.

## Exponential Smoothing

Exponential Smoothing techniques are very similar to ARIMA.

- Holt-Winters Seasonal method for anomaly detection. You should define your seasonal period which can be weeks, months or year, etc. 
- In this case you will need to track several seasonal periods such as having both week and year dependencies together. You should only select one. Usually, it will be the shortest one possible. **(Drawback)**
- Anomaly detection can be done by same statistical tests, as STL or CARTs.

## Neural Networks

- The most suitable type of NN is **LSTM** since we are working with time series.
- This type of **RNN** will allow you to model the **most sophisticated dependencies** in your time series as well as advanced **seasonality dependencies**.
- Can be helpful if you have **multiple** time series **coupled** with each other

## To Keep In Mind's From Website

1. Try the simplest model and algorithm that fit your problem the best.
2. Switch to more advanced techniques if it doesn’t work out.
3. Starting with more general solutions that cover all the cases is a tempting option, but it’s not always the best.

## Sources

[1] Tiunov, Pavel. “Time Series Anomaly Detection Algorithms – Stats and Bots.” *Stats and Bots*, Stats and Bots, 8 June 2017, blog.statsbot.co/time-series-anomaly-detection-algorithms-1cef5519aef2?lipi=urn%3Ali%3Apage%3Ad_flagship3_messaging%3BUw%2FGWSJaTCysr0hAzNNPbw%3D%3D.