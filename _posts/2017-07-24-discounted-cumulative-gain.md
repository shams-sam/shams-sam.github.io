---
layout: post
title: Discounted Cumulative Gain
categories: []
tags: [concept, machine learning, mathematics]
description: Discounted cumulative gain (DCG) is a measure of ranking quality. In information retrieval, it is often used to measure effectiveness of web search engine.
cover: "/assets/images/documents.jpg"
cover_source: "http://opencopy.com/wp-content/uploads/2014/07/file000165248177196dpi.jpg"
comments: true
mathjax: true
---

### [Discounted cumulative gain](https://en.wikipedia.org/wiki/Discounted_cumulative_gain){:target="_blank"}
DCG measures the usefulness, or **gain**, of a document based on its position in the result list. The gain is accumulated from the top of the result list to the bottom, with the gain of each result discounted at lower ranks.

* Measure of **ranking quality**.
* Used to measure effectiveness of search algorithms in **information retrieval**.

* Underlying Assumptions
  * Highly relevant documents are more useful if appearing earlier in search result.
  * Highly relevant documents are more useful than marginally relevant documents which are better than non-relevant documents.

* DCG accumulated at a particular rank position \\(p\\) is given by

$$DCG_p = \sum_{i=1}^p \frac {rel_i} {log_2 (i+1)} = rel_1 + \sum_{i=2}^p \frac {rel_i} {log_2 (i+1)}$$

* Alternative formulation of DCG that places stronger emphasis on retrieving relevant documents is given by

$$DCG_p = \sum_{i=1}^p \frac {2^{rel_i} - 1} {log_2 (i+1)}$$

* Both the alternatives are same if relevance values are binary i.e \\(rel_i \in \\{0, 1\\}\\)

* Various formulations use \\(log_e\\) instead of \\(log_2\\).

* **Logarithmic scale** for reduction provides a smooth reduction curve and hence is used.

* DCG is a successor of **Cumulative Gain**.

### Cumulative Gain

* Does not include the position of a result in the calculation of gain of the result set.
* CG at a particular rank position \\(p\\) is given by

\\[CG_p = \sum_{i=1}^p rel_i\\]

  * Where \\(rel_i\\) is the graded relevance of result at position \\(i\\).

* So, CG is unaffected by changes in ordering of search results and hence, DCG is used for more accurate measure.

### Normalized DCG
Comparing a search algorithms performance from one query to the next cannot be consistently achieved using DCG alone, so the cumulative gain at each position for a chosen value of \\(p\\) should be normalized across queries. This is done by sorting all relevant documents in the corpus by their relative relevance, producing the maximum possible DCG through position \\(p\\), also called **Ideal DCG (IDCG)** through that position.

* Normalized DCG (nDCG) is given by 

$$nDCG_p = \frac {DCG_p} {IDCG_p}$$

  * Where

  $$IDCG_p = \sum_{i=1}^{|REL|} \frac {2^{rel_i} - 1} {log_2 (i+1)}$$

  * Where \\(\|REL\|\\) is the list of documents ordered by relevance in the corpus up to position p.

* The average of nDCG for all queries gives a measure of average performance of ranking algorithms in the search process.

* For a **perfect ranking algorithm*,

\\[DCG_p = IDCG_p\\]

\\[nDCG_p = 1.0\\]

* Since all nDCG are relative values between 0.0 and 1.0 they are **cross-query comparable**.

* The **main difficulty** encountered in using nDCG is the **unavailability of an ideal ordering** of results when only partial relevance feedback is available.

### Example and Calculations

Given a list of documents, each document is judged on a scale of 0 to 3 where 3 is the most relevant scaling down to 0 which is not relevant.

Let a set of documents, S be 

$$S = \{ D_1, D_2, D_3, D_4, D_5, D_6\}$$

Where relevance score by user survey is given by Relevance Set, R in the same order,

$$R = \{3, 2, 3, 0 , 1, 2\}$$

* CG is given by

$$CG_6 = \sum_{i=1}^6 rel_i = 3 + 2 + 3 + 0 + 1 + 2 = 11$$

  * Changing the order of documents does not change the score.

* DCG using Logarithmic scale for reduction is given by

$$DCG_6 = \sum_{i=1}^6 \frac {rel_i} {log_2 (i+1)} = 3 + 1.262 + 1.5 + 0 + 0.387 + 0.712 = 6.861$$

| i | \\(rel_i\\)| \\(log_2(i+1)\\) | \\(\frac {rel_i} {log_2(i+1)}\\)|
|:-:|:-:|:-:|:-:|
| 1 | 3 | 1 | 3 |
| 2 | 2 | 1.585 | 1.262 |
| 3 | 3 | 2 | 1.5 |
| 4 | 0 | 2.322 | 0 |
| 5 | 1 | 2.585 | 0.387 |
| 6 | 2 | 2.807 | 0.712 |

  * Changing order of documents say \\(D_3\\) and \\(D_4\\) would decrease the score.

* **The performance of this query to another is incomparable in this form since the other query may have more results, resulting in a larger overall DCG which may not necessarily be better. In order to compare, the DCG values must be normalized.**

* nDCG calculation using the ideal order and decrease sort of relevance score

$$Ideal\_Relevance\_Order = \{3, 3, 2, 2, 1, 0\}$$

$$DCG_6 = \sum_{i=1}^6 \frac {rel_i} {log_2 (i+1)} = 3 + 1.893 + 1 + 0.861 + 0.387 + 0 = 7.141$$

| i | \\(rel_i\\)| \\(log_2(i+1)\\) | \\(\frac {rel_i} {log_2(i+1)}\\)|
|:-:|:-:|:-:|:-:|
| 1 | 3 | 1 | 3 |
| 2 | 3 | 1.585 | 1.893 |
| 3 | 2 | 2 | 1 |
| 4 | 2 | 2.322 | 0.861 |
| 5 | 1 | 2.585 | 0.387 |
| 6 | 0 | 2.807 | 0 |

$$nDCG_6 = \frac {DCG_6} {IDCG_6} = {6.861 \over 7.141} = 0.961$$

* **Drawbacks**:
  * Normalized DCG metric does not penalize for bad documents in the result, because results with relevance {1, 1, 1} and {1, 1, 1, 0} both given same nDCG while later is clearly the worse of the two. This can be fixed by adjusting values of relevance. If the relevance scores are **1, 0, -1** instead of **2, 1, 0**  for **Good, Fair, Bad** the issue will be resolved

  * nDCG does not penalize **missing documents**, because results with relevance {1, 1, 1} has same score as {1, 1, 1, 1, 1}. This can be fixed by considering fixed set size and use minimum score for missing documents which would lead to {1, 1, 1, 0, 0} and {1, 1, 1, 1, 1} where later has a higher nDCG. This would be written as **nDCG@5**

  * nDCG does not work well for query comparison when there are several equally good results. This affects the metrics when limited to only first few results. **For example, for queries such as "restaurants" nDCG@1 would account for only first result and hence if one result set contains only 1 restaurant from the nearby area while the other contains 5, both would end up having same score even though latter is more comprehensive.**

## REFERENCES:

<small>[Discounted cumulative gain](https://en.wikipedia.org/wiki/Discounted_cumulative_gain){:target="_blank"}</small>