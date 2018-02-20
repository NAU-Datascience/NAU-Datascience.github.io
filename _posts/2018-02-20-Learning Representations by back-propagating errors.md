---
layout: post
current: post
<!-- cover:  assets/images/welcome.jpg -->
navigation: True
title: Learning Representations by back-propagating errors 
date: 2018-02-20 08:48:00
tags: [Summary, Deep Learning, Paper]
class: post-template
subclass: 'post tag-getting-started'
author: hamza
---
 
 



### By *David E. Rumelhart, Geoffrey E. Hinton & Ronald J Williams*


[Original Paper](http://www.cs.toronto.edu/~hinton/absps/naturebp.pdf)

There have been many attempts to neural network models. But non of them are capable of learning representaions with using more layer. If the input is directly connected to output unit, it is relatively easy to find learning rules that iteratively adjust the weight of the vector to progressively reduce the difference between the actual and desired output. But with the hidden units, learning becomes more interesting and more difficult. In perceptron, there are 'feature analysers' but these are hand design so they do not learn the representations. 

To get the simplest learning procedure, what one can do is;

First, compute the linear function for state of neuron,

Then, calculate the output of that layer by using non-linear function. In this paper what has been introduced is sigmoid function, but they also note that any function with has a bounded derivative will do. 

The aim is to find a set of weights that ensure that for each input vector the output vector as same as desired output vector. If there is a fixed, finite set of input-output cases, the total error in the performance of the network with a particular set of weights can be computed by comparing the actual output and what network calculate. 

To minimize E by gradient decent, it is necessary to compute the partial derivative of E with respect to each weight in the network. This procedure of computing partial derivative from top to bottom, is called backward pass. 

After computing derivative of E, we can find the other derivatives by using chain rule. This means that we know how much a change in the total input (or any other unit in network) to an output unit will affect the error. Then, change each weight by an amount proportional to the accumulated derivative of E with respect to w.  

Family Tree


The most oblivious draw back of the learning procedure is that the error surface may contain, so gradient decent is not guaranteed to find a global minimum. However, experience with many task shows that the network very rarely get stuck in poor local minima that are significantly worse than the global minimum. They found this kind of undesirable behavior in networks that have just enough connection to perform task. Adding few more connection, adds a new dimension which provide paths around the local minima. 

The learning procedure, in its current form, is not plausible model of learning in brains. However, applying the procedure to various tasks shows that interning internal representations can be constructed by gradient decent in weight-space, and this suggest that it is worth looking for more biologically plausible ways of doing gradient decent in neural network. 
