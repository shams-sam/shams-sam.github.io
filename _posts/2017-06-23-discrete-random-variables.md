---
layout: post
title: Discrete Random Variables
categories: []
tags: [mathematics, probability]
description: A random variable is a variable whose value is a numerical outcome of a random phenomenon. A discrete random variable X has a countable number of possible values.
cover: "/assets/images/dice-steam.jpg"
cover_source: "https://myplanning.ca/wp-content/uploads/2016/09/dice-game-black-close-up.jpg"
comments: true
mathjax: true
---

{% include probability.md %}

### Discrete Random Variables

Even though it is named variable, discrete random variable is actually a function that maps the sample space to a set of discrete real values.

$$X : S \rightarrow R \tag{1}$$

* Where
  * X is the random variable
  * S is the sample space
  * R is the set of real numbers

### Probability Mass Function

Probability mass function is the probability defined over a given random variable, i.e., it gives the probability that a discrete random variable is exactly equal to some value in the sample space, S.

* For a random variable X, \\(p(X=c)\\) is denoted as \\(p(c)\\) and the mapping of each value in sample space to their respective probabilities is known as **pmf**.
* For all values c that are not is sample space \\(p(c) = 0\\) because it is pointing to an empty set.

$$0 \leq p(c) \leq 1 \tag{2}$$

### Commutative Distribution Function

Probability defined over an inequality such as \\(X \leq c\\) gives probabilities of all the events that satisfy the condition from \\(-\infty\\) to c i.e. the probability value estimate for X less than or equal to c. Mathematically,

$$CD(c) = \sum_b p(b)\text{ for all } -\infty \leq b \leq c \tag{3}$$

### Explaination

* Set has 5 boys and 5 girls.
* 3 kids selected at random but gender not known.
* X is the random variable that denotes number of girls selected.
* Event c such that \\(X(c) = 3\\) is given by set \\(c = \\{(GGG)\\}\\) i.e. all three girls selected are girls.
* The pmf for random variable X will be as follows:

| a | p(a)| CD(a) |
|:-:|:-:|:-:|
| 0 | 1/12  | 1/12 |
| 1 | 5/12  | 6/12 |
| 2 | 5/12  | 11/12 |
| 3 | 1/12  | 1 |

* Calculations:
  * Number of ways of selecting k kids from total of N kids is given by \\(C_k^N = \frac{N!}{k! (N-k)!}\\) implies \\(C_3^{10} = \frac{10!}{3! (10-3)!} = 120\\) for N = 10 and k = 3.
  * value 1 : a = 0 means that no girl is selected which implies that k boys are selected out of the total B boys. The number of ways this can be accomplished is given by \\(C_k^B = \frac{B!}{k! (B-k)!}\\) implies \\(C_3^5 = \frac{5!}{3! (5-3)!} = 10\\) for B = 5 and k = 3.
  * For commutative distribution \\(CD(2) = p(0) + p(1) + p(2) = 11/12\\).
  * Similarly the value of \\(p(a)\\) and \\(CD(a)\\) at other values of \\(a\\) can be calculated.


### Random Variable Metrics

**Expected Value**

The average or mean value calculated over all the possible outcomes of the random variable.

\\[E(X) = \sum_n v_i * p(v_i) \tag{3}\\]

  * X is the random variable.
  * \\(v_i\\) is the value the random variable takes with probability \\(p(v_i)\\).
  * sample space size is  n.
  * often represented by \\(\mu\\).
  * it is a measure of central tendency of the random variable.
  * Some other properties of expected value of a random variable:

$$E(X+Y) = E(X) + E(Y) \tag{4}$$

$$E(cX + d) = c * E(X) + d \label{5} \tag{5}$$

**Variance and Standard Deviation**
    
Variance gives the dispersion of probability mass around the mean value (i.e. E(X), expected value) of the random variable.

\\[Var(X) = E((X-\mu)^2) \tag{6}\\]
\\[\sigma = \sqrt (Var(X)) \tag{7}\\]

  * \\(\sigma\\) is the standard deviation.
  * Some other properties of variance of a random variable:

\\[Var(X) = E(X^2) - (E(X))^2 \label{8} \tag{8}\\]
\\[Var(aX + b) = a^2 Var(X) \label{9} \tag{9}\\]
\\[Var(X+Y) = Var(X) + Var(Y) \text{ iff X and Y are independent } \tag{10}\\]

**Derivation of equation \eqref{8}**

$$
  \begin{align}
    Var(X) & = E((X- \mu)^2) \\
    & = E((X - E(X))^2) \\
    & = E(X^2 - 2XE(X) + E(X)^2) \\
    & = E(X^2) - 2E(X) E(X) + E(X)^2 \\
    & = E(X^2) - E(X)^2
  \end{align}
$$

**Derivation of equation \eqref{9} using equations \eqref{5}, \eqref{8}**

$$
  \begin{align}
    Var(aX + b) & = E((aX + b)^2) - (E(aX + b))^2 \\
    & = E(a^2X^2 + 2abX + b^2) - (aE(X) + b)^2 \\
    & = a^2 E(X^2) + 2abE(X) + b^2 - a^2 E^2(X) - 2abE(X) - b^2 \\
    & = a^2 (E(X^2) - E^2(X)) \\
    & = a^2 Var(X)
  \end{align}
$$


### Some Specific Distributions

**Uniform Distribution**

  * All outcomes are eqully possible. 
  * Eg: Probability of getting a heads or tails for a fair coin. 
  * Uniform(N) implies N outcomes and each has probability 1/N.

**Bernoulli Distribution**

  * Used to model the random experiment where each trail has exactly 2 possible outcomes.
  * One possible outcome is termed as success and other as failure.
  * Parameter \\(p\\) is the probability of success in an experiment.
  * Random variable \\(X \in \\{0, 1\\}\\).
  * X = 1 has probability \\(p\\) and X = 0 has probability \\(1-p\\) where 0 is denoting failure and 1 denoting success.

**Binomial Distribution**

  * Used to model \\(n\\) independent traits of Bernoulli Distribution.
  * If X follows Binomial(n, p) then, X = k implies, the event of k successes in n independent Bernoulli trials.

  \\[P(X=k) = C_k^n * (p^k) * ((1-p)^{n-k})\\]

  * \\(C_k^n\\) is the number of ways of picking k success events in n total trials.
  * \\((p^k) * ((1-p)^{n-k})\\) gives the combined probability of the n Bernoulli trails.

**Geometric Distribution**

  * Also defined over Bernoulli distribution.
  * Models the event of k failures before first success.
  * \\(geometric(p)\\) is given by 

  \\[P(X=k) = (1-p)^k * p\\]

  where \\(X = k\\) is the event where first success occured after k failures.

  * If X and Y follows geometric distribution with same probability p, then \\(X + Y\\) is also a geometric distribution.


**Expected Value and Variance for Distributions**

| Distribution | E(X)| Var(X) |
|:-:|:-:|:-:|
| Uniform | \\(\frac{n+1}{2}\\)  | \\(\frac{n^2-1}{12}\\) |
| Bernoulli | \\(p\\) | \\(p(1-p)\\) |
| Binomial | \\(np\\)  | \\(np(1-p)\\) |
| Geometric | \\(\frac{1-p}{p}\\) | \\(\frac{1-p}{p^2}\\) |



## REFERENCES:

<small>[Discrete Random Variables](https://www.hackerearth.com/practice/machine-learning/prerequisites-of-machine-learning/discrete-random-variables/tutorial/){:target="_blank"}</small>
<small>[Expectation and Variance](https://revisionmaths.com/advanced-level-maths-revision/statistics/expectation-and-variance){:target="_blank"}</small>
<small>[Variance](https://en.wikipedia.org/wiki/Variance){:target="_blank"}</small>
