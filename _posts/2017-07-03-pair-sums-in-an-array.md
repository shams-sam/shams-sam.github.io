---
layout: post
title: Pair Sums In An Array
categories: []
tags: [array algorithms, references, algorithms]
cover: "/assets/images/algorithm.png"
cover_source: "https://www.pixelstalk.net/mathematics-hd-desktop-wallpapers/"
description: To find a pair in an array that add up to a given number.
comments: true
---

### Q: Given an array find a pair of element with the given sum.

#### Input:

```python
a = [8, 7, 2, 5, 3, 1]
s = 10
```

#### Output:

```python
(8, 2)
(7, 3)
```

#### Algorithms:

* **Hashing**:
  * Complexity:
    * Time:     O(n)
    * Space:    O(n)

```python
a = [8, 7, 2, 5, 3, 1]
s = 10

h = {}
for idx, elem in enumerate(a):
    h[elem] = idx
    diff = h.get(s-elem, None)
    if diff != None and diff != idx:
        print((elem, s-elem))
```

* **Sorting**:
  * Complexity:
    * Time:     O(nlogn)
    * Space:    O(1)

```python
a = [8, 7, 2, 5, 3, 1]
s = 10

a.sort()
l = 0
h = len(a) - 1

while (l<h):
    temp = a[l] + a[h]
    if temp == s:
        print((a[l], a[h]))
        l = l+1
        h = h-1
    elif temp > s:
        h = h-1
    else:
        l = l+1
```

## REFERENCES:

<small>[500 Data Structures and Algorithms practice problems and their solutions](https://techiedelight.quora.com/500-Data-Structures-and-Algorithms-practice-problems-and-their-solutions){:target="_blank"}</small>
<small>[Find pair with given sum in the array](http://www.techiedelight.com/find-pair-with-given-sum-array/){:target="_blank"}</small>
