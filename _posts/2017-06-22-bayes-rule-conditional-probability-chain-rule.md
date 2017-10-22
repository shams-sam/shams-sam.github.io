---
layout: post
title: Conditional Probability and Bayes' Rule
categories: []
tags: [mathematics, probability]
description: Bayes' theorem calculates the probability of an event based on the prior knowledge of the conditions that might affect the event.
cover: "/assets/images/venn-diagram.jpg"
cover_source: "http://wallpaperswide.com/venn_diagram-wallpapers.html"
comments: true
mathjax: true
---

{% include probability.md %}

### Conditional Probability

The probability of event X given that Y has already occurred is denoted by \\(P(X\|Y)\\)

* If X and Y are **independent**: \\(P(X\|Y) = P(X)\\) because event X is not dependent on event Y.

* If X and Y are **mutually exclusive**: \\(P(X\|Y) = 0\\) because X and Y are disjoint events.

### Product Rule

$$P(X \cap Y) = P(X|Y)*P(Y) \label{1} \tag{1}$$
  
From \eqref{1}, following can be concluded,

* \\(X \subseteq Y\\) implies \\(P(X\|Y) = P(X)/P(Y)\\) because \\(X \cap Y = X\\)
* \\(Y \subseteq X\\) implies \\(P(X\|Y) = 1\\) because \\(X \cap Y = Y\\)

The **distributive, associative** and [**De Morgan's laws**](https://en.wikipedia.org/wiki/De_Morgan%27s_laws){:target="_blank"} are valid for conditional probability.
  
\\[P(X \cup Y\|Z) = P(X\|Z) + P(Y\|Z) - P(X \cap Y\|Z)\\]
\\[P(X^{c}\|Z) = 1-P(X\|Z)\\]

### Chain Rule

$$P(\bigcap_{i=1,..,n}E_{i}) = P(E_{n}|\bigcap_{i=1,..,n-1}E_{i})*P(\bigcap_{i=1,..,n-1}E_{i})$$

### Bayes' Theorem

$$P(Y|X) = \frac{P(X|Y)*P(Y)}{P(X)}$$
  
Where \\(P(X) = P(X \cap Y) + P(X \cap Y^{c})\\) from the sum rule.

### Derivation of Bayes' Theorem

From \eqref{1},

$$P(X \cap Y) = P(X|Y)*P(Y) \label{2} \tag{2}$$

$$P(Y \cap X) = P(Y|X)*P(X) \label{3} \tag{3} $$
  
Using the commutative law, 

$$P(X \cap Y) = P(Y \cap X) \label{4} \tag{4}$$

From \eqref{2}, \eqref{3} and, \eqref{4}, 

$$ P(Y|X) * P(X) = P(X|Y) * P(Y) \tag{5}$$

Hence,

$$P(Y|X) = \frac{P(X|Y)*P(Y)}{P(X)} \tag{6}$$

### EXAMPLE
* \\(p_ot\\) is probability of reaching on time when no car trouble.
* \\(p_ct\\) is probability of car trouble.
* Commute by train if car trouble occurs.
* N is the number of trains available.
* Only 2 of the N trains would reach on time.
* What is the probability of reaching on time.

* Explaination:
  * \\(O\\): reach on time
  * \\(C^c\\): car not working
  * \\(P(O) = P(O \cap C) + P(O \cap C^c)\\)
  * \\(P(O \cap C) = P(O\|C) * P(C) \text{ where } P(C) = 1 - P(C^c)\\)
  * \\(P(O \cap C^c) = P(O\|C^c) * P(C^c) \text{ where } P(O\|C^c) = 2/N\\)


```python
p_ct = float(input()) # P(Car Trouble)
p_ot = float(input()) # P(On Time | No Car Trouble)
N = float(input()) # Number of trains
p_rt = 2.0/N # P(Correct Train)
p_o = p_ct * p_rt + (1-p_ct) * p_ot # P(On Time)
print("%.6f" % p_o)
```



## REFERENCES:

<small>[Bayes’ rules, Conditional probability, Chain rule](https://www.hackerearth.com/practice/machine-learning/prerequisites-of-machine-learning/bayes-rules-conditional-probability-chain-rule/tutorial/){:target="_blank"}</small>
