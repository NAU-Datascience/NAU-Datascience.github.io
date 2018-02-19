---
layout: post
current: post
<!-- cover:  assets/images/welcome.jpg -->
navigation: True
title: "Book Summary Ch 1: The Machine Learning Landscape"
date: 2018-02-19 16:55:00
tags: [Summary, Data Science]
class: post-template
subclass: 'post tag-data-science'
author: bedir
---

# Summary: Hands-On Machine Learning with Scikit-Learn & TensorFlow

I am thinking of creating series of blog posts throughout my journey following this wonderful book. I will try to include everything that I find interesting, useful or really important. I will not change the content a lot, mostly I will summarize with authors (Aurelien Geron) own words, but in places that I see that needs additional comments or if the part is too long to take into summary I will add my own words (I will try to do it as less as possible.) Enjoy...

# Chapter 1: The Machine Learning Landscape

## Table of Contents

1. [What is Machine Learning](#What is Machine Learning)
2. [Why use Machine Learning](#Why use Machine Learning)
3. [Types of Machine Learning Systems](#Types of Machine Learning Systems)
   1. [Supervised/Unsupervised Learning](#Supervised/Unsupervised Learning)
      1. [Supervised learning](#Supervised learning)
      2. [Unsupervised Learning](#Unsupervised Learning)
      3. [Semisupervised Learning](#Semisupervised Learning)
      4. [Reinforcement Learning](#Reinforcement Learning)
   2. [Batch and Online Learning](#Batch and Online Learning)
      1. [Batch learning](#Batch learning)
      2. [Online learning](#Batch learning)
   3. [Instance Based vs Model Based Learning](#Instance Based vs Model Based Learning)
      1. [Instance Based learning](#Instance Based learning)
      2. [Model Based Learning](#Model Based Learning)
4. [Main Challenges of Machine Learning](#Main Challenges of Machine Learning)
   1. [Insufficient Quantity of Training Data](#Insufficient Quantity of Training Data)
   2. [Nonrepresentative Training Data](#Nonrepresentative Training Data)
   3. [Poor Quality Data](#Poor Quality Data)
   4. [Irrelevant Features](#Irrelevant Features)
   5. [Overfitting the Training data](#Overfitting the Training data)
   6. [Underfitting the Training data](#Underfitting the Training data)
5. [Testing and Validating](#Testing and Validating)

## What is Machine Learning

> Field of study that gives computer the ability to learn without being explicitly programmed. 
>
> ​												*— Arthur Samuel, 1959*

## Why use Machine Learning

- Problems for which existing solutions require a lot of hand tuning or long list of rules: One ML algorithm can often simplify code and perform better.
- Complex problems for which there is no good solution at all using traditional approaches: The best ML techniques can find a solution.
- Fluctuating environments: A ML system can adapt to new data.
- Getting insights about complex problems and large amounts of data.

## Types of Machine Learning Systems

- We categorize them according to three identities:
  - Trained with human supervision (How much): Supervised, unsupervised, semi-supervised and reinforcement learning.
  - Incrementally or on the fly: Online vs Batch learning
  - Comparing data points or detecting patterns and build a model for predictions: Instance-based vs model-based learning
- The categories are not distinct from each other, they can be combined. ex. Online, model-based, supervised system.

### Supervised/Unsupervised Learning

#### Supervised learning

- The training data includes the desired solutions, called labels.
- Classification and Regression are two typical tasks.
- Some regression algorithms can be used for classification and vice versa.
- Some important supervised algorithms are:
  - kNN
  - Linear Regression
  - Logistic Regression
  - SVMs
  - Decision Trees and Random Forests
  - Neural Networks

#### Unsupervised Learning

- The training data is unlabeled
- Some important unsupervised algorithms are:
  - Clustering: Try to detect similar groups.
    - k-Means
    - Hierarchical Cluster Analysis (HCA)
    - Expectation Maximization
  - Visualization: Understand how the data is organized and perhaps identify some unsuspected patterns. and dimensionality reduction: Simplify the data without losing too much information.
    - Principal Component Analysis (PCA)
    - Kernel PCA
    - Locally-Linear Embedding (LLE)
    - t-distributed Stochastic Neighbor Embedding (t-SNE)
  - Association rule Learning: Dig into large data and discover the interesting relation between attributes.
    - Apriori
    - Eclat
- Another important unsupervised task is anomaly detection. Helps to determine outliers and unusualities in data.

#### Semisupervised Learning

- Semisupervised algorithms can deal with partially labeled data. ex. Google Photos

#### Reinforcement Learning

- The learning system, called an agent, can observe the environment, select and perform actions, and get reward in return. It must learn the best strategy called policy.
- ex. Deepmind - AlphaGo

### Batch and Online Learning

- Whether or not the system can learn incrementally from a stream of incoming data.

#### Batch learning

- The system is incapable of learning incrementally; it must be trained using all the data available.
- Generally takes a lot of time and computing resources.
- First trained and then launched.
- All the data is needed to retrain the system.
- May not be able to use if the data is really huge.

#### Online learning

- You train the system incrementally by feeding it data instances sequentially, either individually or by small groups called mini-batches. Each step is fast and cheap, so the system can learn on the fly.
- Great system for continuous flow.
- You can get rid of the data after using it.
- One important parameter of this system is how fast they should adapt to changing data: this is called learning rate. If it is high, the system will adapt better but will forget quickly. If it is low, will learn slower, but less sensitive to noise in the new data. 
- With new data, your system's performance may decrease.

### Instance-Based vs Model-Based Learning

#### Instance-Based learning

- The system learns examples by heart and then generalizes to new cases using similarity measure.

#### Model-Based learning

- Another way to generalize from a set of examples is to build a model of these examples, then use that to make predictions. This is called mode based learning.
- How can you know which values will make your model perform best? To answer this question, you need to specify a performance measure. You can either define a utility function (fitness function) that measures how good your model is, or you can define a cost function that measures how bad it is.
- Typical ML project:
  - You study the data
  - You select a model
  - You train in on the training data
  - Finally, you apply the model to make predictions on new cases (inference)

## Main Challenges of Machine Learning

Two things that can go wrong are Bad Data, Bad Algorithm...

### Insufficient Quantity of Training Data

- It takes a lot of data for most Machine Learning algorithms to work properly.
- If you don't have enough data, none of the other things that you can do can save your system…

### Nonrepresentative Training Data

- In order to generalize well, it is crucial that your training data be representative of the new cases you want to generalize to.
- Sampling bias: Systematic error due to a non-random sample of a population
- ex. US Presidental Election 1936, the Literary Digest's biased poll

### Poor Quality Data

- If your training data is full of errors, outliers, and noise, it will make it harder for system to detect underlying patterns, so your system is less likely to perform well.

### Irrelevant Features

- A critical part of the Machine Learning project is coming up with a good set of features to train on. This process called feature engineering involves:
  - Feature selection: Selecting the most useful features.
  - Feature extraction: Combining existing features to produce a more useful one.
  - Creating new features by gathering new data.

### Overfitting the Training data

- The model performs well on the training data, but it does not generalize well.
- Overfitting happens when the model is too complex relative to the amount and noisiness of the training data. The possible solutions are:
  - To simplify the model by selecting one with fewer parameters, by reducing the number of attributes in the training data or by constructing the model.
  - To gather more training data
  - To reduce the noise in the training data
- Constraining a model to make it simpler and reduce the risk of overfitting is called regularization.
- You want to find the balance between fitting the data perfectly and keeping the model simple enough to ensure that it will generalize well.
- The amount of regularization to apply during learning can be controlled by a hyperparameter. A hyperparameter is a parameter of a learning algorithm (not of the model). 
- Tuning hyperparameters is an important part of building a Machine Learning system.

### Underfitting the Training data

- Opposite of overfitting the data.
- It occurs when your model is too simple to learn the underlying structure of the data.
- Main options to fix this problem are:
  - Selecting more powerful model, with more parameters.
  - Feeding better features to the learning algorithm.
  - Reducing the constraints on the model.

## Testing and Validating

- The only way to know how well a model will generalize to new cases is to actually try it out on new cases.
- Split the data: Training set and test set
- The error rate on new cases is called the generalization error (or out of sample error), and by evaluating your model on the test set, you get an estimation of this error. This value tells you how well your model performs on instances that it has never seen before.
- If the training error is low and generalization error is high that means that your model is overfitting.
- It is common to use 80% of the data for training and hold out 20% for testing.
- To solve the issue of overfitting hyperparameters for the test data, you can divide the data to 3, adding validation set to existing ones.
- Train multiple models with various hyperparameters using the training set, you select the model and hyperparameters that perform best on the validation set, and when you are happy with your model you run a single final test against the test set to get an estimate of the generalization error.
- To avoid 'wasting' too much training data in validation sets, use cross-validation: The training set is split into complementary subsets, and each model is trained against a different combination of these subsets, and each model is trained against a different combination of these subsets and validated against the remaining parts. Next final model is trained using these hyperparameters on the full training set.

