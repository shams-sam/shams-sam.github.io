---
layout: post
title: Cost Function of Linear Regression
categories: []
tags: [machine learning, andrew ng]
description: Linear regression is a linear approach for modeling the relationship between a scalar dependent variable y and one or more explanatory variables (or independent variables) denoted X
cover: "/assets/images/regression.jpeg"
cover_source: "https://cdn-images-1.medium.com/max/1440/1*VoNxmH8kRLKlNI_uuEoBvw.jpeg"
comments: true
mathjax: true
---

### Linear Regression
Linear regression is an approach for modeling the relationship between a **scalar dependent variable** y and one or more **explanatory variables** (or **independent variables**) denoted X. The case of one explanatory variable is called **simple linear regression** or **univariate linear regression**. For more than one explanatory variable, the process is called **multiple linear regression**.
In linear regression, the relationships are modeled using **linear predictor functions** whose unknown model parameters are estimated from the data. Such models are called linear models.


### Hypothesis
The hypothesis for a univariate linear regression model is given by, 

$$h_\theta (x) = \theta_0 + \theta_1\,x \tag{1}$$

* Where 
  * \\(h_\theta (x)\\) is the hypothesis function, also denoted as \\(h(x)\\) sometimes
  * \\(x\\) is the independent variable
  * \\(\theta_0\\) and \\(\theta_1\\) are the parameters of the  linear regression that need to be learnt

### Parameters of the Hypothesis
In the above case of the hypothesis, \\(\theta_0\\) and \\(\theta_1\\) are the parameters of the hypothesis. In case of a univariate linear regression, \\(\theta_0\\) is the **y-intercept** and \\(\theta_1\\) is the **slope** of the line.

Different values for these parameters will give different hypothesis function based on the values of slope and intercepts.

### Cost Function of Linear Regression

![Linear Regression](/assets/2017-08-11-cost-function-of-linear-regression/fig-1-linear-regression.png?raw=true){:height="300px" width="450px"}

Assume we are given a dataset as plotted by the 'x' marks in the plot above. The aim of the linear regression is to find a line similar to the blue line in the plot above that fits the given set of training example best. Internally this line is a result of the parameters \\(\theta_0\\) and \\(\theta_1\\). So the objective of the learning algorithm is to find the best parameters to fit the dataset i.e. **choose \\(\theta_0\\) and \\(\theta_1\\) so that \\(h_\theta (x)\\) is close to y for the training examples (x, y)**. This can be mathematically represented as,

$$minimize_{\theta_0, \theta_1} {1 \over 2m} \sum_{i=1}^m \left( h_\theta(x^{(i)}) - y^{(i)} \right)^2 \tag{2}$$

* Where
  * \\(h_\theta(x^{(i)}) = \theta_0 + \theta_1\,x^{(i)} \\)
  * \\((x^{(i)},y^{(i)})\\) is the \\(i^{th}\\) training data
  * m is the number of training example
  * \\({1 \over 2}\\) is a constant that helps cancel 2 in derivative of the function when doing calculations for gradient descent

So, **cost function** is defined as follows, 

$$J(\theta_0, \theta_1) = {1 \over 2m} \sum_{i=1}^m \left( \hat{y^{(i)}} - y^{(i)} \right)^2 = {1 \over 2m} \sum_{i=1}^m \left( h_\theta(x^{(i)}) - y^{(i)} \right)^2 \tag{3}$$

which is basically \\( {1 \over 2} \bar{x}\\) where \\(\bar{x}\\) is the mean of squares of \\(h_\theta(x^{(i)}) - y^{(i)}\\), or the difference between the predicted value and the actual value.

And **learning objective is to minimize the cost function** i.e.

$$minimize_{\theta_0, \theta_1} J(\theta_0, \theta_1) \tag{4}$$

This cost function is also called the **squared error function** because of obvious reasons. It is the most commonly used cost function for linear regression as it is simple and performs well.

### Understanding Cost Function

Cost function and Hypthesis are two different concepts and are often mixed up. Some of the key differences to remember are,

| Hypothesis \\(h_\theta(x)\\) | Cost Function \\(J(\theta_1)\\)|
|:-:|:-:|
| For a fixed value of \\(\theta_1\\), function of x | Function of parameter \\(\theta_1\\)  |
| Each value of \\(\theta_1\\) corresponds to a different hypothesis as it is the slope of the line | For any such value of \\(\theta_1\\), \\(J(\theta_1)\\) can be calculated using (3) by setting \\(\theta_0 = 0\\) |
| It is a linear line or a hyperplane | Squared error cost function given in (3) is convex in nature |

Consider a simple case of hypothesis by setting \\(\theta_0 = 0\\), then (1) becomes

$$h_\theta (x) = \theta_1\,x \tag{5}$$

which corresponds to different lines passing through the origin as shown in plots below as y-intercept i.e. \\(\theta_0\\) is nulled out. 

![Simple Hypothesis](/assets/2017-08-11-cost-function-of-linear-regression/fig-2-simple-hypothesis.png?raw=true){:height="300px" width="400px"}

For the given training data, i.e. x's marked on the graph, one can calculate cost function at different values of \\(\theta_1\\) using (3) which can be expressed in the following form using (5),

$$J(\theta_1) = {1 \over 2m} \sum_{i=1}^m \left( \theta_1\,x^{(i)} - y^{(i)} \right)^2 \tag{6}$$

At \\(\theta_1 = 2\\),

$$J(2) = {1 \over 2 * 3} (1^2 + 2^2 + 3^2) = {14 \over 6} = 2.33$$

At \\(\theta_1 = 1\\),

$$J(1) = {1 \over 2 * 3} (0^2 + 0^2 + 0^2) = 0$$

At \\(\theta_1 = 0.5\\),

$$J(1) = {1 \over 2 * 3} (0.5^2 + 1^2 + 1.5^2) = 0.58$$

On plotting points like this further, one gets the following graph for the cost function which is dependent on parameter \\(\theta_1\\).

![Simple Hypothesis](/assets/2017-08-11-cost-function-of-linear-regression/fig-3-cost-function.png?raw=true){:height="300px" width="400px"}

In the above plot each value of \\(\theta_1\\) corresponds to a different hypothesis. The **optimization objective** was to minimize the value of \\(J(\theta_1)\\) from (4), and it can be seen that the hypothesis correponding to the minimum \\(J(\theta_1)\\) would be the best fitting straight line through the dataset.

The issue lies in the fact that we cannot always find the optimum global minima of the plot manually because **as the number of dimensions increase, these plots would be much more difficult to visualize and interpret**. So there is a need of an automated algorithm that can help achieve this objective.


## REFERENCES:

<small>[Machine Learning: Coursera - Cost Function](https://www.coursera.org/learn/machine-learning/lecture/rkTp3/cost-function){:target="_blank"}</small><br>
<small>[Machine Learning: Coursera - Cost Function Intuition I](https://www.coursera.org/learn/machine-learning/lecture/N09c6/cost-function-intuition-i){:target="_blank"}</small><br>
<small>[Linear Regression: Wikipedia - Cost Function](https://en.wikipedia.org/wiki/Linear_regression){:target="_blank"}</small>
