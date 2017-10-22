---
layout: post
title: Regularized Logistic Regression
tags: [machine learning, andrew ng]
description: Regularization is a process of introducing additional information in order to solve an ill-posed problem or to prevent overfitting
cover: "/assets/images/overfitting.png"
cover_source: "https://upload.wikimedia.org/wikipedia/commons/thumb/1/19/Overfitting.svg/1200px-Overfitting.svg.png"
comments: true
mathjax: true
---

### Introduction
The intuition and implementation of logistic regression is implemented in [Classifiction and Logistic Regression]({% post_url 2017-08-31-classification-and-representation %}){:target="_blank"} and [Logistic Regression Model]({% post_url 2017-09-02-logistic-regression-model %}){:target="_blank"}

Similar to the linear regression, even logistic regression is prone to overfitting if there are large number of features. If the decision boundary is overfit, the shape might be highly contorted to fit only the training data while failing to generalise for the unseen data.

So, the cost function of the logistic regression is updated to penalize high values of the parameters and is given by, 

$$ J(\theta) = -{1 \over m} \sum_{i=1}^m \left( y^{(i)}\,log(h_\theta(x^{(i)}) + (1-y^{(i)})\,log(1 - h_\theta(x^{(i)})) \right) + {\lambda \over 2m } \sum_{j=1}^n \theta_j^2 \tag{1}$$

* Where 
  * \\({\lambda \over 2m } \sum_{j=1}^n \theta_j^2\\) is the **regularization term**
  * \\(\lambda\\) is the **regularization factor**


~~~python
import numpy as np
mul = np.matmul

"""
X is the design matrix
y is the target vector
theta is the parameter vector
lamda is the regularization parameter
"""

def sigmoid(X):
    return np.power(1 + np.exp(-X), -1)

"""
hypothesis function
"""
def h(X, theta):
    return sigmoid(mul(X, theta))

"""
regularized cost function
"""
def j(theta, X, y, lamda=None):
    m = X.shape[0]
    theta[0] = 0
    if lamda:
        return (-(1/m) * (mul(y.T, np.log(h(X, theta))) + \
                          mul((1-y).T, np.log(1 - h(X, theta)))) + \
                (lamda/(2*m))*mul(theta.T, theta))[0][0] 
    return -(1/m) * (mul(y.T, np.log(h(X, theta))) + \
                     mul((1-y).T, np.log(1 - h(X, theta))))[0][0]
~~~

### Regularization for Gradient Descent

Previously, the **gradient descent for logistic regression without regularization** was given by,

$$
  \begin{align}
    \text{repeat until convergence}
    \begin{cases}
      \theta_j := \theta_j - \alpha {1 \over m} \sum_{i=1}^m \left(h(x^{(i)}) - y^{(i)} \right) x_j^{(i)}
    \end{cases}
  \end{align}
$$

* Where \\(j \in \\{0, 1, \cdots, n\\} \\)

But since the equation for cost function has changed in (1) to include the regularization term, there will be a **change in the derivative of cost function** that was plugged in the gradient descent algorithm,

$$
  \begin{align}
    \frac {\partial} {\partial \theta_j} J(\theta) &= \frac {\partial} {\partial \theta_j} \left[-{1 \over m} \sum_{i=1}^m \left( y^{(i)}\,log(h_\theta(x^{(i)}) + (1-y^{(i)})\,log(1 - h_\theta(x^{(i)})) \right) + {\lambda \over 2m } \sum_{j=1}^n \theta_j^2 \right] \\
    &= {1 \over m} \sum_{i=1}^m \left( h_\theta(x^{(i)}) - y^{(i)} \right) x_j^{(i)} + \frac {\lambda} {m} \theta_j \\
  \end{align}
$$

Because the first term of cost fuction remains the same, so does the first term of the derivative. So taking **derivative of second term** gives \\(\frac {\lambda} {m} \theta_j\\) as seen above.

So, (2) can be updated as, 

$$
  \begin{align}
    \text{repeat until convergence}
    \begin{cases}
      \theta_0 &:= \theta_0 - \alpha \left[ {1 \over m} \sum_{i=1}^m \left( h_\theta(x^{(i)}) - y^{(i)} \right) x_0^{(i)} \right] \\
      \theta_j &:= \theta_j - \alpha \left[ {1 \over m} \sum_{i=1}^m \left( h_\theta(x^{(i)}) - y^{(i)} \right) x_j^{(i)} + \frac {\lambda} {m} \theta_j \right] \\
    \end{cases}
  \end{align}
$$

* Where \\(j \in \\{1, 2, \cdots, n\\} \\) and h is the **sigmoid function**


It can be noticed that, **for case j=0, there is no regularization term** included which is consistent with the convention followed for 
regularization.

~~~python
"""
regularized cost gradient
"""
def j_prime(theta, X, y, lamda=None):
    m = X.shape[0]
    theta[0] = 0
    if lamda:
        return (1/m) * mul(X.T, (h(X, theta) - y)) + (lamda/m) * theta 
    return (1/m) * mul(X.T, (h(X, theta) - y)) 

"""
Simultaneous update
"""
def update_theta(theta, X, y, lamda=None):
    return theta - alpha * j_prime(theta, X, y, lamda)

~~~

Link to [Rough Working Code](https://github.com/shams-sam/logic-lab/blob/master/CourseraMachineLearningAndrewNg/LogisticRegressionHigherOrder.ipynb){:target="_blank"}. Change the value of lamda in the code to get different decision boundaries for the [data](https://github.com/shams-sam/logic-lab/blob/master/CourseraMachineLearningAndrewNg/logistic_regression_data_2.csv){:target="_blank"} as shown below.

![Regularization with \\(\lambda = 0.01\\)](\assets\2017-09-15-regularized-logistic-regression\fig-1-regularization.png?raw=true)
![Regularization with \\(\lambda = 0.1\\)](\assets\2017-09-15-regularized-logistic-regression\fig-2-regularization.png?raw=true)
![Regularization with \\(\lambda = 1\\)](\assets\2017-09-15-regularized-logistic-regression\fig-3-regularization.png?raw=true)
![Regularization with \\(\lambda = 10\\)](\assets\2017-09-15-regularized-logistic-regression\fig-4-regularization.png?raw=true)
![Regularization with \\(\lambda = 100\\)](\assets\2017-09-15-regularized-logistic-regression\fig-5-regularization.png?raw=true)

## REFERENCES:

<small>[Machine Learning: Coursera - Logistic Regression Model](https://www.coursera.org/learn/machine-learning/lecture/4BHEy/regularized-logistic-regression){:target="_blank"}</small>