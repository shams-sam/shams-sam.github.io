---
layout: post
title: Regularized Linear Regression
categories: []
tags: [machine learning, andrew ng]
description: Regularization is a process of introducing additional information in order to solve an ill-posed problem or to prevent overfitting
cover: "/assets/images/overfitting.png"
cover_source: "https://upload.wikimedia.org/wikipedia/commons/thumb/1/19/Overfitting.svg/1200px-Overfitting.svg.png"
comments: true
mathjax: true
---

The intuition of regularization are explained in the previous post: [Overfitting and Regularization]({% post_url 2017-09-08-overfitting-and-regularization %}){:target="_blank"}. The cost function for a regularized linear equation is given by,

$$J(\theta) = {1 \over 2m} \left[ \sum_{i=1}^m \left( h_\theta(x^{(i)}) - y^{(i)} \right)^2 + \lambda \sum_{j=1}^n \theta_j^2 \right] \tag{1}$$

* Where
  * \\(\lambda \sum_{i=1}^n \theta_j^2\\) is the regularization term
  * \\(\lambda\\) is called the **regularization parameter**

### Regularization for Gradient Descent

Previously, the **gradient descent for linear regression without regularization** was given by,

$$
  \begin{align}
    \text{repeat until convergence}
    \begin{cases}
      \theta_j := \theta_j - \alpha \left[ {1 \over m} \sum_{i=1}^m \left( h_\theta(x^{(i)}) - y^{(i)} \right) x_j^{(i)} \right]
    \end{cases}
  \end{align}
  \tag{2}
$$

* Where \\(j \in \\{0, 1, \cdots, n\\} \\)

But since the equation for cost function has changed in (1) to include the regularization term, there will be a **change in the derivative of cost function** that was plugged in the gradient descent algorithm,

$$
  \begin{align}
    \frac {\partial} {\partial \theta_j} J(\theta) &= \frac {\partial} {\partial \theta_j} \left ({1 \over 2m} \left[ \sum_{i=1}^m \left( h_\theta(x^{(i)}) - y^{(i)} \right)^2 + \lambda \sum_{i=1}^n \theta_j^2 \right] \right) \\
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

* Where \\(j \in \\{1, 2, \cdots, n\\} \\)

It can be noticed that, **for case j=0, there is no regularization term** included which is consistent with the convention followed for 
regularization.

The second equation in the gradient descent algorithm above can be written as, 

$$\theta_j := \theta_j \left(1 - \alpha {\lambda \over m} \right) - \alpha {1 \over m} \left[ \sum_{i=1}^m \left( h_\theta(x^{(i)}) - y^{(i)} \right) x_j^{(i)}\right]$$

* Where \\(\left(1 - \alpha {\lambda \over m} \right) \lt 1\\) because \\(\alpha\\) and \\(\lambda\\) are both positive. 

The **implementation** from [Mulivariate Linear Regression]({% post_url 2017-08-23-multivariate-linear-regression %}){:target="_blank"} can be updated with the following **updated regularized functions for cost function, its derivative, and updates**. One, can notice that \\(theta_0\\) has not been handled seperately in the code. And as expected it **does not affect the regularization** much. It can be implemented in the conventional way by adding a couple of logical expressions to the function 

~~~python
"""
Regularized Version
"""
def reg_j_prime_theta(data, theta, l, order_of_regression, i):
    result = 0
    m = len(data)
    for x, y in data :
        x = update_features(x, order_of_regression)
        result += (h(x, theta) - y) * x[i]
    result += l*theta[i]
    return (1/m) * result

def reg_j(data, theta, l, order_of_regression):
    cost = 0
    m = len(data)
    for x, y in data:
        x = update_features(x, order_of_regression)
        cost += math.pow(h(x, theta) - y, 2)
    reg = 0
    for j in theta:
        reg += math.pow(j, 2)
    reg = reg * l
    return (1/(2*m)) * (cost + reg)

def reg_update_theta(data, alpha, theta, l, order_of_regression):
    temp = []
    for i in range(order_of_regression+1):
        temp.append(theta[i] - alpha * reg_j_prime_theta(data, theta, l, order_of_regression, i))
    theta = np.array(temp)
    return theta

def reg_gradient_descent(data, alpha, l, tolerance, theta=[], order_of_regression = 2):
    if len(theta) == 0:
        theta = np.atleast_2d(np.random.random(order_of_regression+1) * 100).T
    prev_j = 10000
    curr_j = reg_j(data, theta, l, order_of_regression)
    print(curr_j)
    cost_history = []
    theta_history = [] 
    counter = 0
    while(abs(curr_j - prev_j) > tolerance):
        try:
            cost_history.append(curr_j)
            theta_history.append(theta)
            theta = reg_update_theta(data, alpha, theta, l, order_of_regression)
            prev_j = curr_j
            curr_j = reg_j(data, theta, l, order_of_regression)
            if counter % 100 == 0:
                print(curr_j)
            counter += 1
        except:
            break
    print("Stopped with Error at %.5f" % prev_j)
    return theta, cost_history, theta_history
reg_theta, reg_cost_history, reg_theta_history = reg_gradient_descent(data, 0.01, 1, 0.0001, order_of_regression=150)
~~~

The following plot is obtained on running a random experiment with **regression of order 150**, which clearly shows how the regularized hypothesis is much better fit to the data.

![Regularizated Linear Regression](/assets/2017-09-11-regularized-linear-regression/fig-1-regularized-linear-regression.png?raw=true)

### Regularization for Normal Equation

The equation and derivation of Normal Equation can be found in the post [Normal Equation]({% post_url 2017-08-28-normal-equation %}){:target="_blank"}. It is given by, 

$$\theta = \left( X^TX \right)^{-1}X^Ty$$

But after adding the regularization term as shown in (1), making very small changes in the derivation in the [post]({% post_url 2017-08-28-normal-equation %}){:target="_blank"}, one can reach the result for regularized normal equation as shown below,

$$\theta = \left( X^TX + \lambda \cdot L\right)^{-1}X^Ty$$

* Where 
  * **I is the identity matrix**
  * \\(L = \begin{bmatrix} 0 & 0 & \cdots &  0 \\\\ 0 & 1 & \cdots & 0 \\\\ \vdots & \vdots & \ddots & \vdots \\\\ 0 & 0 & \cdots & 1 \\\\ \end{bmatrix} \\) is a **square matrix** of size (n+1)

If \\(m \le n\\), then the \\(X^TX\\) was **non-invertible in the unregularized case** but, \\(X^TX + \lambda I\\) does not face the same issues and is **always invertible**.

The effect of regularization on regression using normal equation can be seen in the following plot for **regression of order 10**.

![Regularizated Linear Regression](/assets/2017-09-11-regularized-linear-regression/fig-2-regularization-for-normal-equation.png?raw=true)

> No implementation of regularized normal equation presented as it is very straight forward.

## REFERENCES:

<small>[Machine Learning: Coursera - Regularized Linear Regression](https://www.coursera.org/learn/machine-learning/lecture/QrMXd/regularized-linear-regression){:target="_blank"}</small>
