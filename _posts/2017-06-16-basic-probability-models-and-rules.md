---
layout: post
title: Basic Probability Concepts
categories: []
tags: [mathematics, probability]
description: Probability is a number between 0 and 1, where, 0 indicates impossibility and 1 indicates certainty.
cover: "/assets/images/monty-hall-problem.jpg"
cover_source: "https://sc5.io/wp-content/uploads/2016/04/montyhall_16_9_still.jpg"
comments: true
mathjax: true
---

{% include probability.md %}


### Introduction
* **Trail or Experiment** - The act that leads to a result with certain possibility.
* **Sample Space**	- Set of all possible outcomes of an experiment.
* **Event** -	Non empty subset of a sample space.

### Basic Probability Formula

\\[P(A) = \sum_{i=1}^n P(E_i) \label{1} \tag{1} \\]

Where A is an event, S is the sample space, \\(E_1 ... E_n\\) are the n outcomes in A.

If \\(E_1 ... E_n\\) are equally likely to occur, then \eqref{1} can be written as,

\\[P(A) = {\text{number of outcomes in A} \over \text{total number of possible outcomes}} \label{2} \tag{2}\\]

From \eqref{2}, following results can be inferred,

* \\(0 \leq P(A) \leq 1\\),
* \\(P(S) = 1\\)

### Complement of an Event

Compliment of an event A is defined as all the outcomes of the sample space, S that are not in A, i.e.

\\[P(A^c) = 1 - P(A) \tag{3} \\]

Where \\(A^c\\) is used to denote the compliment of A.

### Union and Intersection of Events

\\[P(A \cup B) = P(A) + P(B) + P(A \cap B) \label{4} \tag{4}\\]

### Mutually Exclusive Events

Two events A and B are mutually exclusive if there are no overlapping outcomes, i.e., the intersection of the two experiments is a null set.

\\[P(A \cap B) = 0 \label{5} \tag{5}\\]

Using \eqref{4} and \eqref{5}, 

 $$P(A \cup B) = P(A) + P(B) \tag{6}$$

### Independent Events

Two events A and B are independent if occurence of one does not affect the probability of the other occuring and is mathematically given by,

\\[P(A \cap B) = P(A) * P(B)\\]

### Sum Rule or Marginal Probability

\\[P(A) = \sum_{B} P(\text{A and B})\\]

### EXAMPLE
* M wants to go fishing this weekend to nearby lake.
* His neighbour A is also planing to go to the same spot for fishing this weekend.
* The probability that it will rain this weekend is \\(p_1\\).
* There are two possible ways to reach the fishing spot (bus or train).
* The probability that
  * M will take the bus is \\(p_{mb}\\)
  * A will take the bus is \\(p_{ab}\\).
* Travel plans of both are independent of each other and rain.
* What is the probability \\(p_{rs}\\) that M and A meet each other only (should not meet in bus or train) on a lake in rain ?

```python
p_mb = float(input()) # P(M taking Bus)
p_ab = float(input()) # P(A taking Bus)
p_1 = float(input()) # P(Rain)
p_rs = p_1 * (1 - p_ab*p_mb - (1-p_ab)*(1-p_mb)) # P(Meet at lake only)
print("%.6f" % p_rs)
```

## REFERENCES:

<small>[Basic Probability Models and Rules](https://www.hackerearth.com/practice/machine-learning/prerequisites-of-machine-learning/basic-probability-models-and-rules/tutorial/){:target="_blank"}</small>
