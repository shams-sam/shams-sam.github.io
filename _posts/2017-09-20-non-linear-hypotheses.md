---
layout: post
title: Non-linear Hypotheses
categories: []
tags: [machine learning, andrew ng]
description: Advantages of neural networks over logistic regession and the relationship between the two. Neural network is essentially the successor of logistic regression.
cover: "/assets/images/abstract.png"
cover_source: "https://maxoffsky.com/word/wp-content/uploads/2014/04/Screen-Shot-2014-04-28-at-10.32.16-AM.png"
comments: true
mathjax: true
---


### Drawbacks of Logistic Regression
Consider a highly **non-linear classification** task, say something similar to the one shown in the plot below. In order to achieve a decision boundary like the one plotted, one needs to introduce **non-linear features** in the form of quadratic and other higher order terms, similar to the equation below.

![Non-linear Classification](/assets/2017-09-20-non-linear-hypotheses/fig-1-non-linear-classification.png?raw=true)

$$h(\theta) = g(\theta_0 + \theta_1\,x_1 + \theta_2\,x_2 + \theta_3\,x_1\,x_2 + \theta_4\,x_1^2\,x_2 + \theta_5\,x_1^3\,x_2 + \cdots)$$

As the number of features increase then **number of terms in the hypotheses would also increase exponentially** to get a good fit which would have **high probability of overfitting** the data. Hence, when the number of features is really high and the decision boundary is complex, logistic regression would not generalize the solution very well by leveraging the power of polynomial terms. So for highly complex tasks like the ones where one needs to classify objects from images, logistic regression would not perform well.

For example, for images of size 100 * 100 pixels if one uses all quadratic features, there would be around 50 million parameter values to learn which is computationally very expensive task and still not a guarantee of good decision boundary.

This is where **Neural Networks** step in to save the day.

### Neural Networks
They are class of **very powerful machine learning classifiers** that are capable of fitting almost any hypotheses and are **motivated by the way a brain functions**. Even though the concepts of neural networks were well developed by the 80s, they came into popularity fairly recently because of the advances in the **compute power of machines using multiple cores and GPUs**. It is mainly because neural networks are a class of very **computationally expensive algorithms** and earlier systems were just not fast enough to get good results in a feasible time-frame.

### One Learning Algorithm Hypothesis
This hypothesis puts light on the fact that even though human brain learns a variety of tasks involving visual, vocal, or audio inputs, it does not learn them using different algorithms. It has been found that if the optic nerve is re-routed to the auditory cortex (responsible for decoding audio), it would learn to use the input and work with visual input as well i.e. **Auditory cortex learns to see.** So, extending the result of such experiments suggesting that a single tissue in brain is capable of performing different tasks like analyse visuals, audio, touch etc, it is posited that there must be **one algorithm that can approximate any learning task similar to the way brain learns**.


## REFERENCES:

<small>[Machine Learning: Coursera - Non-Linear Hypotheses](https://www.coursera.org/learn/machine-learning/lecture/OAOhO/non-linear-hypotheses){:target="_blank"}</small><br>
<small>[Machine Learning: Coursera - Neurons and the Brain](https://www.coursera.org/learn/machine-learning/lecture/IPmzw/neurons-and-the-brain){:target="_blank"}</small>