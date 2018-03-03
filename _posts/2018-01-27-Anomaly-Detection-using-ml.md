---
layout: post
current: post
<!-- cover:  assets/images/welcome.jpg -->
navigation: True
title: Anomaly Detection of Time Series Data using Machine Learning & Deep Learning
date: 2018-01-27 9:00:00
tags: [Summary, Data Science]
class: post-template
subclass: 'post tag-getting-started'
author: bedir

---



_This is a summary of a blog post, published on medium.com._

**Original Blog Post:** [XenonStack - Jul 3, 2017](https://medium.com/@xenonstack/anomaly-detection-of-time-series-data-using-machine-learning-deep-learning-c248061ea4f5?lipi=urn%3Ali%3Apage%3Ad_flagship3_messaging%3BUw%2FGWSJaTCysr0hAzNNPbw%3D%3D)

## What is Time Series Data

Time series data is informations taken at a particular duration. For instance, having a set of sensor data observed at particular equal paces, each sensor can be classified as time series. If the data is collected without any order in time, or at once, it is not time series data.

There are two types of time series data:

**1- Stock Series** (Measure of attribute, in particular point of time)

**2- Flow Series** (Measure of activity, in a time interval)

**PS:** Most common application of time series, is forecasting.

## Components of Time Series Data

For us to analyse time series data, we need to know the different pattern types. These patterns will together create the set of observations on time series.

**1- Trend**: A long pattern present in the time series. It represents the variations of low, medium and high frequency filtered out from the time series. (-)

If there is no increasing or decreasing pattern in the time series data, it is taken as **stationary** in the mean.

There are two types of trend pattern:

- **Deterministic** In this case, the effects of shocks present in the time series are eliminated. (-)
- **Stochastic** It is the process in which the effects of shocks are never eliminated as they have permanently changed the level of the time series.

**2- Cyclic:** The pattern exhibit up and down movements around a specified trend. The period of time is not fixed and usually composed of at least 2 months in duration.

**3- Seasonal:** Pattern that reflects regular fluctuations. These short-term movements occur due to the seasonal and custom factors of people. The data faces regular and predictable changes which occurs on regular intervals of calendar. It always consist of fixed and known period.

The main sources of seasonality:

- Climate
- Institutions
- Social habits and practices
- Calendar

**Models** to create a seasonal component in time series:

- **Additive Model **— It is the model in which the seasonal component is added with the trend component.
- **Multiplicative** **Model **— In this model seasonal component is multiplied with the intercept if trend component is not present in the time series.

**4- Irregular:**  It is an unpredictable component of time series.

## Time Series Data vs Cross-Section Data

Time Series Data is composed of collection of data of one specific variable at particular interval of time. On the other hand, Cross-Section Data is consist of collection of data on multiple variables from different sources at a particular interval of time.

Collection of company’s stock market data at regular interval of year is an example of time series data. But when the collection of company’s sales revenue, sales volume is collected for the past 3 months then it is taken as an example of cross-section data.

Time series data is mainly used for obtaining results over an extended period of time but, cross-section data focuses on the information received from surveys at a particular time.

## What is Time Series Analysis?

Analysis is performed in order to understand the structure and functions produced by the time series.

Two approaches are used for analyzing time series data are -

- In the time domain
- In the frequency domain

Time series analysis is mainly used for -

- Decomposing the time series
- Identifying and modeling the time-based dependencies
- Forecasting
- Identifying and model the system variation

## Need of Time Series Analysis

In order to model successfully, the time series is important in machine learning and deep learning. Time series analysis is used to understand the internal structure and functions that are used for producing the observations. Time Series analysis is used for -

- **Descriptive **  Patterns are identified in correlated data. In other words, the variations in trends and seasonality in the time series are identified.
- **Explanation ** Understanding and modeling of data is performed.
- **Forecasting ** The prediction from previous observations are performed for short term trends.
- **Invention An alysis ** Effect performed by any event in time series data, is analyzed.
- **Quality Control **  When the specific size deviates, it provides an alert. (-)

## Applications of Time Series Analysis

![img](https://cdn-images-1.medium.com/max/1600/1*LxaU50nxL1Kx6M_0K49JOg.jpeg)

## Time Series Database

Time series database is a software which is used for handling the time series data. Highly complex data such as higher transactional data, is not feasible for the relational database management system. Many relational systems does not work properly for time series data. Therefore, time series databases are optimised for the time series data. Various time series databases are given below -

- CrateDB
- Graphite
- InfluxDB
- Informix TimeSeries
- Kx kdb+
- Riak-TS
- RRDtool
- OpenTSDB

## What is Anomaly?

**Anomaly** is defined as something that deviates from the normal behaviour or what is expected. The anomaly is a kind of contradictory observation in the data. It gives the proof that certain model or assumption does not fit into the problem statement.

### Different Types of Anomalies

- **Point Anomalies ** If the specific value within the dataset is anomalous with respect to the complete data then it is known as Point Anomalies.
- **Contextual Anomalies ** If the occurrence of data is anomalous for specific circumstances, then it is known as Contextual Anomalies. For example, the anomaly occurs at a specific interval of period.
- **Collective Anomalies  **If the collection of occurrence of data is anomalous with respect to the rest of the dataset then it is known as Collective Anomalies. For example, breaking the trend observed in ECG.

## Models of Time Series Data

**ARIMA Model **  ARIMA stands for Autoregressive Integrated Moving Average. Auto Regressive (AR) refers as lags of the differenced series, Moving Average (MA) is lags of errors and it represents the number of difference used to make the time series stationary. (-)

**Assumptions** followed while implementing ARIMA Model

- **Time series data should posses stationary property:** this means that the data should be independent of time. Time series consist of cyclic behaviour and white noise is also taken as stationary.
- **ARIMA model is used for a single variable.** The process is meant for regression with the past values. (-)

In order to **remove non-stationarity** from the time series data the steps given below are followed

- Find the difference between the consecutive observations.
- For stabilizing the variance log or square root of the time series data is computed.
- If the time series consists of the trend, then the residual from the fitted curve is modulated.

ARIMA model is used for predicting the future values by taking the linear combination of past values and past errors. The ARIMA models are used for modeling time series having random walk processes and characteristics such as trend, seasonal and nonseasonal time series.

**Holt-Winters **  It is a model which is used for **forecasting** the **short term period**. It is usually applied to achieve exponential smoothing using additive and multiplicative models along with increasing or decreasing trends and seasonality. Smoothing is measured by beta and gamma parameters in the holt’s method.

- When the beta parameter is set to FALSE, the function performs exponential smoothing.
- The gamma parameter is used for the seasonal component. If the gamma parameter is set to FALSE, a non-seasonal model is fitted.

## How to find Anomaly in Time Series Data

**AnomalyDetection R package **

It is a robust open source package used to find anomalies in the presence of seasonality and trend. This package is build on Generalised E-Test and uses Seasonal Hybrid ESD (S-H-ESD) algorithm. S-H-ESD is used to find both local and global anomalies. This package is also used to detect anomalies present in a vector of numerical variables. Is also provides better visualization such that the user can specify the direction of anomalies.

**Principal Component Analysis **

**It is a statistical technique used to reduce higher dimensional data into lower dimensional data without any loss of information.** Therefore, this technique can be used for developing the model of anomaly detection. This technique is **useful** at that time of situation **when sufficient samples are difficult to obtain**. So, PCA is used in which model is trained using available features to obtain a normal class and then distance metrics is used to determine the anomalies.

**Chisq Square distribution **

It is a kind of statistical distribution that constitutes 0 as minimum value and no bound for the maximum value. Chisq square test is implemented for detecting outliers from univariate variables. It detects both lowest and highest values due to the presence of outliers on both side of the data.

## What are Breakouts in Time Series Data?

- **Mean shift **  Sudden change in time series. For example the usage of CPU is increased from 35% to 70%. It is added when the time series move from one steady state to another state.
- **Ramp Up ** Sudden increase in the value of the metric from one steady state to another. It is a slow process as compared with the mean shift. It is a slow transition process from one stable state to another.

**PS:** In Time series often more than one breakouts are observed.

## How to detect Breakouts in Time Series Data?

In order to detect breakouts in time series **Twitter** has introduced a package known as **BreakoutDetection** package (opensource). It uses E-Divisive with Medians (EDM) algorithm to detect the divergence within the mean.

## Need of Machine Learning and Deep Learning in Time Series Data

Machine learning techniques are more effective as compared with the statistical techniques. This is because machine learning have two important features such as feature engineering and prediction. The feature engineering aspect is used to address the trend and seasonality issues of time series data. The issues of fitting the model to time series data can also be resolved by it.

Deep Learning is used to combine the feature extraction of time series with the non-linear autoregressive model for higher level prediction. It is used to extract the useful information from the features automatically without using any human effort or complex statistical techniques.

## Anomaly Detection using Machine Learning

Firstly, supervised learning is performed for training data points so that they can be classified into anomalous and non-anomalous data points. But, for supervised learning, there should be labeled anomalous data points.

**Another approach for detecting anomaly is unsupervised learning. One can apply unsupervised learning to train CART so that prediction of next data points in the series could be made. To implement this, confidence interval or prediction error is made. Therefore, to detect anomalous data points Generalised ESD-Test is implemented to check which data points are present within or outside the confidence interval**

The most common supervised learning algorithms are

- Supervised neural networks
- Support vector machine
- K-nearest neighbors
- Bayesian networks
- Decision trees

The most common unsupervised algorithms are

- Self-organizing maps (SOM)
- K-means
- C-means
- Expectation-maximization meta-algorithm (EM)
- Adaptive resonance theory (ART)
- One-class support vector machine

![img](https://cdn-images-1.medium.com/max/1600/1*FWN896X6mtQLOdq77KqNog.jpeg)

### Anomaly Detection using Deep Learning

Recurrent neural network is one of the deep learning algorithm for detecting anomalous data points within the time series. It consist of input layer, hidden layer and output layer. The nodes within hidden layer are responsible for handling internal state and memory. They both will be updated as the new input is fed into the network.  The internal state of RNN is used to process the sequence of inputs. **The important feature of memory is that it can automatically learn the time-dependent features.**



![Anomaly Detection using Deep Learning](https://www.xenonstack.com/blog/static/public/uploads/media/Anamoly-detection-using-Deep-learning.jpg)



## Summary from website

- Time Series is defined as the sequence of data points. The components of time series are responsible for the understanding of patterns of data. In time series, anomalous data points can also be there. 
- Therefore, there is a need to detect them. Various statistical techniques are mentioned in the blog that is used but machine learning and deep learning are essential.  
- In machine learning, supervised learning and unsupervised learning is used for detecting anomalous data. On the other hand, in deep learning recurrent neural network is used.

## Sources

[1] XenonStack. “Anomaly Detection of Time Series Data using Machine Learning & Deep Learning.” *Medium*, Medium, 3 July 2017, medium.com/@xenonstack/anomaly-detection-of-time-series-data-using-machine-learning-deep-learning-c248061ea4f5?lipi=urn%3Ali%3Apage%3Ad_flagship3_messaging%3BUw%2FGWSJaTCysr0hAzNNPbw%3D%3D.