---
layout: post
title: Classification and Logistic Regression
categories: []
tags: [machine learning, andrew ng]
description: Logistic regression, or logit regression, or logit model is a regression model where the dependent variable is categorical
cover: "/assets/images/logistic-regression.png"
cover_source: "http://www.onthelambda.com/wp-content/uploads/2014/07/quadratic.png"
comments: true
mathjax: true
---

### Introduction
Classification is a supervised learning problem wherein the target variable is categorical unlike regression where the target variable is continuous. Classification can be binary i.e. only two possible values of the target variable or multi-class i.e. more than two categories.

The most basic step would be to try and fit regression curve to see if one can achieve classification using the same approach. Below is a plot attempting the same.

![Regression Fit for Classification](/assets/2017-08-31-classification-and-representation/fig-1-regression-for-classification.png?raw=true)

It can be seen below that the attempt to achieve classification using **regression curve and thresholding** will not always yield conclusive results.
In first case say only red data points are in the dataset, then fitting the curve and setting the threshold at 0.5 would work, but say an outlier is present like the blue data point then the same decision boundary D1 would shift to D2 if the threshold is kept constant and the boundary would not be perfect. Hence there is a need of **Decision Boundary** instead of predictive curve.

Applying linear regression to classification problem might work in some cases but is not advisable as it would not scale with complexity.

Another issue with application of linear regession to classification would be that even know the categorical variables are discreet say 1s and 0s, the hypothesis would give continuous values which maybe much greater that 1 or much lesser than 0. This issue can be solved by using **logistic regression** where 

$$0 \leq h_\theta(x) \leq 1 \tag{1}$$

### Logistic Regression

Since (1) is to be true, the hypothesis from linear regression given by \\(h_\theta(x) = \theta^T\,x\\) will not work for logistic regression. Hence there is a need of **squashing function** i.e. a function which limits the output of hypothesis between given range. For logistic regression **sigmoid function is used as the squashing function**. The hypothesis for logistic regression is give by,

$$h_\theta(x) = g(\theta^T\,x) = {1 \over 1 + e^{-\theta^Tx}} \tag{2}$$ 

Where \\(g(z) = {1 \over 1 + e^{-z}}\\) and is called **sigmoid function or logistic function**. Plot of the sigmoid function is given below which shows no matter what the value of x, the function returns a value between 0 and 1 consistent with (1).

![Sigmoid Plot](/assets/2017-08-31-classification-and-representation/fig-2-sigmoid-plot.png?raw=true)

> The value of hypothesis is interpretted as the probability that the input x belongs to class y=1. i.e. probability that y=1, given x, parametrized by \\(\theta\\).

It can be mathematically represented as,

$$h_\theta(x) = P(y=1|x;\theta) \tag{3}$$

The fundamental properties of probability holds here, i.e.,

$$P(y=0|x;\theta) + P(y=1|x;\theta) = 1 \tag{4}$$

### Decision Boundary

for the given hypothesis of logistic regression in (2), say \\(\delta=0.5\\) is chosen as the **threshold for the binary classification**, i.e. 

$$
  \begin{align}
    \text{predict } y &= 1 \text{, if } h_\theta(x) \geq 0.5 \\
    \text{predict } y &= 0 \text{, if } h_\theta(x) \lt 0.5 \\
  \end{align}
  \tag{5}
$$

From the plot of sigmoid function, it is seen that

$$
  \begin{align}
    g(z) \geq 0.5 \text{, if } z \geq 0 \\
    g(z) \lt 0.5 \text{, if } z \lt 0 \\
  \end{align}
  \tag{6}
$$

Using (6), (5) can be rewritten as,
$$
  \begin{align}
    \text{predict } y &= 1 \text{, if } \theta^T\,x \geq 0 \\
    \text{predict } y &= 0 \text{, if } \theta^T\,x \lt 0 \\
  \end{align}
  \tag{7}
$$

![Decision Boundary](/assets/2017-08-31-classification-and-representation/fig-3-decision-boundary.png?raw=true)

Suppose the training data is as show in the plot above where dots and Xs are the two different classes. Let the hypothesis \\(h_\theta(x)\\) and the optimal value of \\(\theta\\) be given by,

$$h_\theta(x) = g(\theta_0 + \theta_1\,x_1 + \theta_2\,x_2)\tag{8}$$

$$\theta = 
  \begin{bmatrix}
    -12 \\ 1 \\ 1 \\
  \end{bmatrix}
  \tag{9}
$$

Using the \\(\theta\\) from (9) and hypothesis from (8) , (7) can be written as,

$$
  \begin{align}
    \text{predict } y &= 1 \text{, if } -12 + x_1 + x_2 \geq 0 \text{ or } x_1 + x_2 \geq 12 \\
    \text{predict } y &= 0 \text{, if } -12 + x_1 + x_2 \lt 0 \text{ or } x_1 + x_2 \lt 12 \\
  \end{align}
$$

If the line \\(x_1 + x_2 = 12\\) is plotted as shown in the plot above then the region below i.e. the yellow region is where \\(x_1 + x_2 \lt 12\\) and predicted 0 and similarly the white region above the line \\(x_1 + x_2 = 12\\) is where \\(x_1 + x_2 \geq 12\\) and hence predicted 1. **The line here is called the decision boundary.** As the name suggests this line seperates the region with prediction 0 from region with prediction 1. **Decision boundary and prediction regions are the property of the hypothesis and not of the dataset**. Dataset is only used to fit the parameters, but once the parameters are determined they solely define the decision boundary

> It is possible to achieve non-linear decision boundaries by using the higher order polynomial terms and can be encorporated in a way similar to how multivariate linear regression handles polynomial regression.

![Non-Linear Decision Boundary](/assets/2017-08-31-classification-and-representation/fig-4-non-linear-decision-boundary.png?raw=true)

The plot above is an example of **non-linear decision boundary** using higher order polynomial logistic regression.

Say, the hypothesis of the logistic regression has higher order polynomial terms, and is given by, 

$$h_\theta(x) = g(\theta_0 + \theta_1\,x_1 + \theta_2\,x_2 + \theta_3\,x_1^2 + \theta_4\,x_2^2) \tag{10}$$

The, \\(\theta\\) given below would form an apt decision boundary,

$$\theta = 
  \begin{bmatrix}
    -1 \\ 0 \\ 0 \\ 1 \\ 1 \\
  \end{bmatrix} \tag{11}
$$

Substituting (12) in (11), 

$$\theta^T x = -1 + x_1^2 + x_2^2$$

So, from (7), the decision boundary is given by, 

$$
  \begin{align}
    -1 + x_1^2 + x_2^2 &= 0 \\
    x_1^2 + x_2^2 &= 1
  \end{align}
$$

Which the equation of a circle at origin with radius 0, as can be seen in the plot above. And, using the \\(\theta\\) from (12) and hypothesis from (11) , (7) can be written as,

$$
  \begin{align}
    \text{predict } y &= 1 \text{, if } -1 + x_1^2 + x_2^2 \geq 0 \text{ or } x_1^2 + x_2^2 \geq 1 \\
    \text{predict } y &= 0 \text{, if } -1 + x_1^2 + x_2^2 \lt 0 \text{ or } x_1^2 + x_2^2 \lt 1 \\
  \end{align}
  \tag{12}
$$

> As the order of features is increased more and more complex decision boundaries can be achieved by logistic regression.

**Gradient Descent is used to fit the parameter values \\(\theta\\) in (9) and (12).**

## REFERENCES:

<small>[Machine Learning: Coursera - Classification](https://www.coursera.org/learn/machine-learning/lecture/wlPeP/classification){:target="_blank"}</small><br>
<small>[Machine Learning: Coursera - Hypothesis Representation](https://www.coursera.org/learn/machine-learning/lecture/RJXfB/hypothesis-representation){:target="_blank"}</small><br>
<small>[Machine Learning: Coursera - Decision Boundary](https://www.coursera.org/learn/machine-learning/lecture/WuL1H/decision-boundary){:target="_blank"}</small><br>
