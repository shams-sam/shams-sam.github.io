---
layout: post
title: Continuous Random Variables
categories: []
tags: [mathematics, probability]
description: A continuous random variable is a random variable where the data can take infinitely many values.
cover: "/assets/images/distributions.jpg"
cover_source: "http://page.mi.fu-berlin.de/werner99/bilder/normalvert3.jpg"
comments: true
mathjax: true
---


{% include probability.md %}

### Continuous Random Variables
A continuous random variable is a function that maps the sample space of a random experiment to an interval in real value space. A random variable is called continuous if there is an underlying function f(x) such that 

$$P(p \leq X \leq q) = \int_p^q f(x) dx \tag{1}$$

  * Where f(x) is a non negative function  called **probability density function (pdf)**

* Probability Density funtion can be considered analogous to Probability Mass function of Discrete random variable but differs in that pdf does give probability directly at a value like in case of pmf. Hence the rules of probability do not apply to f(x).

* Pdf takes value 0 for values outside range(X).

* Also the following property can be inferred from rules of probability, 

$$P(-\infty \leq X \leq \infty) = \int_{-\infty}^\infty f(x) dx = 1$$

* Probability of a continuous random variable taking a range of values is given by the area under the curve of f(x) for that range.

### Cumulative Distribution Function (cdf)
Cdf for continuous random variable is same as the one for discrete random variable. It is given by, 

$$cdf(X \leq c) = \int_{-\infty}^c f(x) dx$$

* **Properties of cdf:**
  * Unlike f(x), cdf(x) is probability and follows the laws and hence,

$$0 \leq cdf(x) \leq 1$$
  
  * As probability is **non-negative**, cdf is a **non-decreasing** function.
  * Differential of cdf is given by 

$$cdf'(x) = f(x)$$

  * Limits of cdf are given by

  $$cdf(x) \to 0 \text{ as } x \to -\infty$$

  $$cdf(x) \to 1 \text{ as } x \to \infty$$

### Some Specific Distributions

* **Uniform Distribution**

\\(X = Uniform(N)\\) is used to model a scenario where all outcomes are equally likely. Uniform([c, d]) is when all the values of \\(x\(c \leq x \leq d\)\\) are equally probable. It is given by

$$ Uniform([c, d]) = {1 \over (d-c)}$$

* **Exponential Distribution**

  * Defined using a parameter \\(\lambda\\) and has the pdf given by

$$ f(x) = \lambda e^{- \lambda x}, \, x \geq 0 $$

  * It is used to model the waiting time for an event to occur eg. waiting time for nuclear decay of radioactive isotope distributed exponentially and \\(\lambda\\) is known as the half life of the isotope.

  * This distribution exhibits lack of memory i.e. when waiting time is modeled using exponential distributions, the probability of it happening in next N minutes remains same irrespective of the time passed.

* **Proof**: According to lack of memory property, prove \\(P(X \gt n+w \| X \gt w ) = P(X \gt n)\\).

$$P(X \gt n+w | X \gt w) = \frac {P(X \gt n+w)} {P(X \gt w)}$$

$$ \frac {P(X \gt n+w)} {P(X \gt w)} = \frac {e^{- \lambda (n+w)}} {e^{- \lambda w}} = e^{- \lambda n}$$

* **Normal Distribution**
  * Most commonly used distribution
  * Also known as Gaussian distribution
  * It is denoted by \\(N(\mu, \sigma^2))\\) where \\(\mu\\) is the mean and \\(\sigma^2\\) is the variance fo the given distribution.
  * Standard Normal Distribution, denoted by Z is a normal distribution with mean = 0 and variance = 1.
  * It is symmetric about the y-axis and follows the bell-curve.
  * It is given by 

  $$N(\mu, \sigma^2) = {1 \over \sigma \sqrt{2 \pi} } e^{ \frac {- (x - \mu)^2} {2 \sigma^2} }$$

### Summary of Distributions

| Distribution | pdf(x)| cdf(x) |
|:-:|:-:|:-:|
| \\(Uni(c, d)\\) | \\({1 \over d-c}\\)  | \\({x-c \over d-c}\\) |
| \\(Exp( \lambda ), \, x \geq 0 \\) | \\( \lambda e^{- \lambda x} \\) | \\(1 - e^{- \lambda x}\\) |
| \\(N(\mu, \sigma^2)\\) | \\({1 \over \sigma \sqrt{2 \pi} } e^{ \frac {- (x - \mu)^2} {2 \sigma^2} }\\)  | \\({1 \over 2}[1 + erf({ x - \mu \over \sigma \sqrt{2} })]\\) |



### Expected Value

* Gives the average or the mean value over all the possible outcomes of the variable.
* Used to measure the centrality of a random variable.

* For a continuous random variable X, whose pdf is \\(f(x)\\), the expected value in the interval [c, d] is given by,

$$E(X) = \int_c^d x\, f(x) dx \tag{2}$$

* Expected value is often denoted by \\(\mu\\).

* \\(f(x)dx\\) denotes the probability value with which X can take the infinitesimal range dx.

* Some other properties of expected value of a random variable:

\\[E(X+Y) = E(X) + E(Y) \tag{3}\\]
\\[E(cX + d) = c * E(X) + d \tag{4}\\]

### Variance and Standard Deviation

* For a continuous random variable X, with Expected value \\(\mu\\), variance is given by,

\\[Var(X) = E((X-\mu)^2) \tag{5}\\]
\\[\sigma = \sqrt (Var(X)) \tag{6}\\]

* Some other properties of variance of a random variable:

\\[Var(X) = E(X^2) - (E(X))^2 \tag{7}\\]
\\[Var(aX + b) = a^2 Var(X) \tag{8}\\]
\\[Var(X+Y) = Var(X) + Var(Y) \text { iff X and Y are independent } \tag{9}\\]

### Quartiles

The value of \\(x\\) for which \\(cdf(x) = p\\) is called \\(p^{th}\\) quartile of X. So, median for the continuous random variable is the \\(0.5^{th}\\) quartile


## REFERENCES:

1. [Continuous Random Variables](https://www.hackerearth.com/practice/machine-learning/prerequisites-of-machine-learning/continuous-random-variables/tutorial/){:target="_blank"}
