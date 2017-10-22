---
layout: post
title: Improvements on Word2Vec
categories: []
tags: [NLP, machine learning, papers]
description: Importance of optimization and its effect on training time for Word2Vec. Effective utilization of Hierarchical Softmax, Negative Sampling and Subsampling of frequent words.
cover: "/assets/images/wordembedding.png"
cover_source: "http://www.deep-solutions.net/blog/wordembeddings/wordembedding.png"
comments: true
mathjax: true
---

{% include distributed-vector-representation.md %}

### Skip-Gram Model
* Training objective of skip-gram model is to deduce word representations that help in predicting the surrounding words in a sentence or a document, i.e. give a sequence of training words \\(w_1, w_2, w_3, ... , w_T\\), the objective is to maximize the average log probability, 

$${1 \over T} \sum_{t=1}^T \sum_{-c \leq j \leq c, j \neq 0} log\,p(w_{t+j} | w_t)$$

  * Where c is the size of the **training context**
  * Larger c results in more training examples and thus higher accuracy, at the expense of the training time.

* Basic skip-gram formulation defines \\(p(w_{t+j}\|w_t)\\) using softmax function

$$p(w_O|w_I) = \frac {exp((v_{w_O}^{'})^T v_{w_I})} {\sum_{w=1}^W exp((v_w^{'})^T v_{w_I})}$$

  * Where
    * \\(v_w\\) and \\(v_w^{\'}\\) are the **input** and **output** vector representations of \\(w\\)
    * \\(W\\) is the number of words in the vocabulary
    * cost of computing \\(\nabla log\,p(w_O\| w_I)\\) is proportional to \\(W\\) which is quite large in order of \\(10^5 - 10^7\\) terms

### Drawbacks of Initial [Word2Vec]({% post_url 2017-07-11-word-to-vector-word-representations %}){:target="_blank"} Proposed


* Training time
* Indifference to word order and inability to represent idiomatic phrases.

### Improvements

* **Hierarchical Softmax**
  * Computationally efficient approximation of full softmax.
  * Advantageous because instead of evaluating W output nodes in the neural network, only need to evaluate \\(log_2(W)\\) nodes.
  * Uses binary tree representation of the output layer with W nodes as its leaves. Each node represents the **relative probability** of its child nodes. So, probability is assigned to a leaf node through **random walk** from root node
  * Each word can be reached by following an appropriate path from the root. Let \\(n(w, j)\\) be the j-th node on the path from the root to w, and let \\(L(w)\\) be the length of this path. So,

  \\[n(w, 1) = root\\]

  \\[n(w, L(w)) = w\\]

  * For any inner child n, let \\(ch(n)\\) be arbitrary fixed child of n and let \\(\unicode{x27E6} x \unicode{x27E7}\\) be 1 if x is true and -1 otherwise, then hierarchical softmax defines \\(p(w_O\|w_I)\\) as 

  $$p(w_O|w_I) = \prod_{j=1}^{L(w) - 1} \sigma (\unicode{x27E6} n(w, j+1) = ch(n(w, j)) \unicode{x27E7} . (v_{n(w, j)}^{'})^T v_{w_I}) $$

    * Where \\(\sigma (x) = {1 \over (1 + exp(-x))}\\)
  * \\(\sum_{w=1}^W p(w\|w_I) = 1\\) is verifiable.

* **Negative Sampling**
  * Alternative to Hierarchical softmax.
  * Based on **Noise Contrastive Estimation(NCE)** which posits that a good model should be able to differentiate data from noise by means of **logistic regression**.
  * NCE approximately maximizes the log probability of softmax, but skip-gram only aims at learning high quality word representations and hence NCE can be simplified.
  * **Negative Sampling (NEG)** is defined as

  $$log \, \sigma ((v_{w_O}^{'})^T v_{w_I}) + \sum_{i=1}^k \unicode{x1D53C}_{w_i \sim P_n(w)} [log\, \sigma (- (v_{w_I}^{'})^T v_{w_I})]$$

  * It replaces the \\(log\, p(w_O \| w_I)\\) term in skip-gram objective

  * Aiming at distinguishing between \\(w_O\\) from draws from noise distribution \\(P_n(w)\\) using logistic regression, where k is the number of negative samples for each data sample, because this use case does not require maximization of the softmax log probability.

  * k value ranges 5-20 for small datasets and 2-5 for large datasets.

  * NCE differs from NEG in that NCE needs the sample and numerical probabilities of the noise distribution, but NEG uses only samples.

  * Both NCE and NEG have \\(P_n(w)\\) as a free parameter but **unigram distribution** U(w) raised to 3/4 power i.e. \\(U(w)^{3/4}/Z\\) is found to outperform other options like **unigram** and **uniform** distribution.

* **Subsampling of frequent words**
  * In a corpus, most frequent words can occur hundreds of millions of time such as the stopwords.
  * These words give little information by co-occuring with other words. Consequently, vector representations of frequent words do not change significantly after training on several million examples.
  * Imbalance between rare and frequent words are thus countered using sub-sampling approach.
  * Each word \\(w_i\\) in the training set is discarded with a probability given by

  $$P(w_i) = 1 - \sqrt (\frac {t} {f(w_i)})$$

  * Where
    * \\(f(w_i)\\) is frequency of word \\(w_i\\)
    * t is a chosen threshold, around \\(10^{-5}\\)
  * Subsampling formula is chosen **heuristically**

* **Learning Phrases**
  * Aim is to learn phrases where in individual words meaning is entirely different when compared to the group of words.
  * Start off by finding words that frequently occur together and infrequently in other contexts.
  * Theoretically, skip-gram model can be trained with all n-grams, but would be a very memory intensive operation.
  * A data driven approach is put forward based on unigram and bigram counts, given by

  $$score(w_i, w_j) = \frac {count(w_i w_j) - \delta} {count(w_i) * count(w_j)}$$

    * Where \\(\delta\\) is a **discounting coefficient** and prevents phrases formed by very infrequent words. The bigrams with score above a given threshold only are used as phrases.

  * Often it is needed to run the process 2-4 times changing the threshold values and seeing the quality of phrases formed.

### Conclusions

* Subsampling results in faster training and significantly better representations of uncommon words.

* Negative sampling helps accurately train for frequent words using a simple method.


## REFERENCES

<small>[Distributed Representations of Words and Phrases and their Compositionality](http://web2.cs.columbia.edu/~blei/seminar/2016_discrete_data/readings/MikolovSutskeverChenCorradoDean2013.pdf){:target="_blank"}</small>