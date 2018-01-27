
---
layout: post
current: post
<!-- cover:  assets/images/welcome.jpg -->
navigation: True
title: Time Series Anomaly Detection
date: 2018-01-27 10:00:00
tags: [Summary, Data Science]
class: post-template
subclass: 'post tag-getting-started'
author: hamza
---

### Detection of Anomalous Drops with Limited Features and Sparse Examples in NoisyHighly Periodic Data

*Dominique T. Shipmon, Jason M. Gurevitch, Paolo M. Piselli, Steve Edwards*

[Link to paper](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/46283.pdf)

## **Summary**

### <u>**About the data**</u>:

* 14 different sets of data where saved 5 min intervals. (288 each day)

### <u>**About the problem**</u>: 

* When there are clear labels for anomalous data a binary classifier can be built predict anomalies and non-anomalouspoints. But in this case we dont have any label! Problem is finding anomalies without using labeled data.

* Since methods like clustering analysis, isolations forests requires labeled data plus they work better when there are many features, paper provides solution using artificial neural networks. 

* Another problem is because what counts as an anomaly can vary based
  on the data, each problem potentially requires its own model.

* One solution they propose is:

  * make prediction using model
  * take euclidean distance between predictions and true value
  * set some threshold value 
  * if distance bigger then threshold, it is anomanly 

  but this could leed to numerous false positives especially with noisy data. 

  (false positive: actualy not anomaly but our prediction says it is anomaly)

* Other two approach is

  * using accumulator 
  * using a probabilistic approach as outlined

### **<u>DETECTION RULES</u>:**

1. Accumulator:

The goal of the accumulator rule was to require multiple point anomalies to occur in a short period of time before signalling a sustained anomaly. They tried two different rules for how a point anomaly is detected, and then tested both of them as part of the accumulator rule.This rule involved a counter that would grow as point anomalies are detected, and shrink in cases where the predicted value is correct. The goal of this is to prevent noise that a local anomaly detection algorithm would incur, by requiring multiple anomalies in a short timeframe to cause it to reach a threshold for signaling. 

* Threshold

  This algorithm defined a local anomaly as any value where the actual value is more than a given delta below the expected value, when the actual value is greater than a hardcoded threshold which says any value above it is not anomalous. 

* Variance Based

  We tried using local variance to determine outages by defining an outage as any value that is outside of 20 times the rolling variance from the current prediction, so that noisy areas would allow for more noise in anomalies. However, this method proved to be slightly less effective than the simple threshold.

they found that threshold accumulator rule is working more effective on their datasets, they used that in all of anomaly detection for this paper.  observed that the accumulator rules frequently identified false positives after peaks due to an offset in the models inference compared to the ground-truth. This offset is likely due to training on a previous months where changes in periodicity could occur gradually into the next evaluation month. In an attempt to abate these false positives, we added a parameter for ‘peak values’ that would decrement the accumulator by three following a peak, and allowing the accumulator to go below 0 (down to a negative the threshold). However, we only wanted this to affect prediction immediately after peaks, so the accumulator would decay back to 0 if more non-anomalous data points are found, effectively preventing it from predicting an anomaly immediately after a peak.

For all of our models we defined the threshold for a non-anomalous value at 0.3, a peak value at 0.35, had a an accumulator threshold at 15 and had the delta for a local outage at 0.1 

​		

2. GaussianTailProbability

The second anomaly detection rule is the Gaussian tail probability rule. The raw anomaly score calculation is simply the difference between the inference and ground-truth. Because they are only checking the lack of activity, they take out the negative scores.

the series of resulting raw anomaly scores are used to calculate the rolling mean and varience.  The rolling mean has two windows where the length of W2 < W1. The two rolling means and variance are used to calculate the tail probability which is the final anomaly likelihood score.

**<u>Example pipeline for Gaussian Tail Probability</u>** 

**I'm by no means certain that this implementation is correct, though!** Any assistance in verifying this would be most welcome !!!

```python
# Data
seq_len = 50
x = np.zeros([4000,seq_len,1])
y = np.zeros([4000,1])
for i in tqdm(range(4000)):
    x[i] = data[i:i+seq_len]
    y[i] = data[i+seq_len]
    
    
# LSTM 

net = tflearn.input_data(shape=[None, seq_len, 1])
net = tflearn.lstm(net, 64, return_seq=True, activation='elu')
net = tflearn.dropout(net, 0.5)
net = tflearn.lstm(net, 64, activation='elu')
net = tflearn.dropout(net, 0.5)
net = tflearn.fully_connected(net, 1, activation='linear')
net = tflearn.regression(net, optimizer='adam', loss='mean_square',
                       learning_rate=0.001)

model = tflearn.DNN(net, tensorboard_verbose=2)
model.fit(x, y, n_epoch=10,  show_metric=True, snapshot_step=100)


```

![](/Users/D/Desktop/plot1.png)

``` python
dif = (true_y - y_preds)
dif = np.maximum(dif,0)![plot2](/Users/D/Desktop/plot2.png)
def rolling_window(a, window):
    shape = a.shape[:-1] + (a.shape[-1] - window + 1, window)
    strides = a.strides + (a.strides[-1],)
    return np.lib.stride_tricks.as_strided(a, shape=shape, strides=strides)

rolling_mean = np.mean(rolling_window(dif,3), -1)


dif_mean = np.mean(rolling_mean)
dif_std = np.std(rolling_mean)
gausian_rolling = (rolling_mean-dif_mean)/dif_std
out=[]
for i in rolling_mean:
    ceil = (dif_mean + 3 * dif_std)
    floor= (dif_mean - 3 * dif_std)
    if i>ceil or i<floor:
        out.append(i)

```



![](/Users/D/Desktop/plot2.png)



### **<u>PREDICTION MODELS</u>**		

* Baseline = Threshold model


  ​	

| **Anomaly rule** | Accumulator | Tail Probabilty | Intersection |
| :--------------: | :---------: | :-------------: | :----------: |
|        TN        |    7833     |      8211       |     8211     |
|        FN        |     183     |       366       |     366      |
|        TP        |     246     |       63        |      63      |
|        FP        |     378     |        0        |      0       |

* Fourier Series (a Fourier series is a way to represent a function as the sum of simple sine waves)	

![](/Users/D/Desktop/Screen Shot 2018-01-27 at 12.38.12 PM.png)

| **Anomaly rule** | Accumulator | Tail Probabilty | Intersection |
| :--------------: | :---------: | :-------------: | :----------: |
|        TN        |    7797     |      8009       |     8072     |
|        FN        |     375     |       429       |     429      |
|        TP        |     54      |        0        |      0       |
|        FP        |     414     |       202       |     139      |

* DNN 

  ​	Num_layer = 10

  ​	Layer_size = 200

  ​	activation = Relu6

  ​	batchsize = 200 

  ​	num_step = 1200

  ​	optimizer = Adam

  ​	learning_rate = 0.0001

| **Anomaly rule** | Accumulator | Tail Probabilty | Intersection |
| :--------------: | :---------: | :-------------: | :----------: |
|        TN        |    7751     |      8003       |     8077     |
|        FN        |     348     |       410       |     415      |
|        TP        |     81      |       19        |      14      |
|        FP        |     460     |       208       |     134      |



- RNN

  ​	Num_layer = 10

  ​	Layer_size = 75

  ​	activation =  ELU

  ​	batchsize = 200 

  ​	num_step = 2500

  ​	optimizer = Adam

  ​	learning_rate = 0.0001

| **Anomaly rule** | Accumulator | Tail Probabilty | Intersection |
| :--------------: | :---------: | :-------------: | :----------: |
|        TN        |    6889     |      8056       |     8100     |
|        FN        |     409     |       416       |     418      |
|        TP        |     20      |       13        |      11      |
|        FP        |    1322     |       155       |     111      |

* LSTM

  Num_layer = 10

​	Layer_size = 70

​	activation =  ELU

​	batchsize = 200 

​	num_step = 2500

​	optimizer = Adam

​	learning_rate = 0.001

| **Anomaly rule** | Accumulator | Tail Probabilty | Intersection |
| :--------------: | :---------: | :-------------: | :----------: |
|        TN        |    7801     |      7951       |     8083     |
|        FN        |     388     |       419       |     420      |
|        TP        |     41      |       10        |      9       |
|        FP        |     410     |       260       |     128      |



### **<u>Findings</u>**

1.  The first is that in every instance, the intersection between the accumulator method and the tail probability method reduced the amount of false positives flagged by the model. However, since the intersection makes a tighter bound around anomalous regions, the true positive rate is also decreased.
2. The second important finding is that there is a very small difference between all of our neural network models with regards to their detection confusion matrices.		

### **<u>Conclusion</u>**

*  the Fourier was slightly more effective than the others, this can also be due to the data itself	
* With access to more features, deep learning could provide even more accurate results. Results
  suggest that due to the limited set of features available it didn’t provide significant advantages to simpler periodic models.
* Room for further experimentation can be done by trying even more anomaly detection methods and seeing if another combination can work even better than the two we propose here.