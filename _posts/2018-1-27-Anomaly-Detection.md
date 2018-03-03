---
layout: post
current: post
<!-- cover:  assets/images/tags.jpg -->
navigation: True
title: Anomaly Detection
date: 2018-01-27 08:00:00
tags: [Summary, Data Science]
class: post-template
subclass: 'post tag-getting-started'
author: nadide

---


[LINK](https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/anomaly-detection)


- Rare events, finding unusual data points
- Encompasses many important tasks in ML
    - Identifying transactions that are potentially fraudulent
    - Learning patterns that indicate a network intrusion has occurred
    - Finding abnormal clusters of patients
    - Checking values input to a system


#### Modules for an anomaly detection model
- [One-Class Support Vector Machine](### One-Class Support Vector Machine): Creates a one-class Support Vector Machine model for anomaly detection, \>100features, aggressive boundary
- [PCA-Based Anomaly Detection](### PCA-Based Anomaly Detection): Creates an anomaly detection model using Principal Component Analysis, Fast training

------------------------------------------------------------

### One-Class Support Vector Machine

[LINK](https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/one-class-support-vector-machine)

- Particularly useful in scenarios where you have a lot of "normal" data and not many cases of the anomalies you are trying to detect (Ex: fraudulent transactions)

> Note: The module creates a kernel-SVM model, which means that it is not very scalable. If training time is limited, or you have too much data, you can use other methods such as PCA-Based Anomaly Detection.

#### Understanding

- Support vector machines (SVMs)
    - Supervised learning, used for both classification and regression tasks
    - The SVM algorithm is given a set of training examples labeled as belonging to one of two classes
    - Oversampling is used to replicate the existing samples so that you can create a two-class model, but it is impossible to predict all the new patterns of fraud or system faults from limited examples 
- Therefore, in __one-class SVM__, has only one class, which is the “normal” class 
- From normal class properties can predict which examples are unlike the normal examples. 

#### Configuration

- η, represents the upper bound on the fraction of outliers ([nu-property](https://www.microsoft.com/en-us/research/publication/estimating-the-support-of-a-high-dimensional-distribution/?from=http%3A%2F%2Fresearch.microsoft.com%2Fpubs%2F69731%2Ftr-99-87.pdf))
    - lets you control the trade-off between outliers and normal cases
- ε (epsilon), value to use as the stopping tolerance.
    - affects the number of iterations used when optimizing the model, and depends on the stopping criterion value

 _Single Parameter_, a specific set of values as arguments  
 _Parameter Range_, specifying multiple values and using a parameter sweep to find the optimal configuration 


------------------------------------------------------------

### PCA-Based Anomaly Detection

[LINK](https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/pca-based-anomaly-detection)


- Use in scenarios where it is easy to obtain training data from one class, such as valid transactions, but difficult to obtain sufficient samples of the targeted anomalies.
- By using the PCA-Based Anomaly Detection module, you can train the model using the available features to determine what constitutes a "normal" class, and then use distance metrics to identify cases that represent anomalies.


#### Understanding

- Principal Component Analysis (PCA)
    - ML technique can be applied to feature selection and classification
    - Used in exploratory data analysis, reveals the inner structure of the data and explains the variance in the data
    - Analyze data that contains multiple variables, all possibly correlated, and determine some combination of values that best captures the differences in outcomes. Then outputs the combination of values into a new set of values called _principal components_.
    - In the case of __anomaly detection__, 
         - First computes projection on the eigenvectors, then computes the normalized reconstruction error. 
         - This normalized error is the anomaly score. 
         - The higher the error, the more anomalous the instance is.
         
#### Configuration

- Number of components to use in PCA (or Range)
    - The decision of how many components to include is an important part of experiment design using PCA
    - Should not include the same number of PCA components as there are variables. Start with some smaller number of components and increase them until some criteria is met
        - If you are unsure of what the optimum value, use parameter range
        - If you manually specify a value, make sure that the number of output components is less than the number of feature columns available in the dataset.
- Amount of oversampling
    - A single integer that represents the ratio of oversampling of the minority class over the normal class (series of interger, range)
    - Imbalanced data makes it difficult to apply standard PCA techniques. By specifying some amount of oversampling, you can increase the number of target instances.
    
>If you specify 1, no oversampling is performed.
>If you specify any value higher than 1, additional samples are  generated to use in training the model.
>However, you cannot view the oversampled data set.

- Enable input feature mean normalization, to normalize all input features to a mean of zero
- Normalization or scaling to zero is generally recommended for PCA, because the goal of PCA is to maximize variance among variables.
- Some additional steps
    - Ensure that a score column is available in both datasets
    - Ensure that label columns are marked
    - Normalize scores from different model types






