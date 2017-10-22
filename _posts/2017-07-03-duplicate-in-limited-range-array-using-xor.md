---
layout: post
title: Duplicate In Limited Range Array (XOR)
categories: []
tags: [array algorithms, references, algorithms]
cover: "/assets/images/algorithm.png"
cover_source: "https://www.pixelstalk.net/mathematics-hd-desktop-wallpapers/"
description: One way to find the duplicate in a limited range array using XOR operation.
comments: true
---

### Q: Find duplicate in limited range (1 to n-1) array of size n using XOR operation.

#### Input:

```python
a = [1, 2, 3, 4, 4]
```

#### Output:

```python
4
```

#### Algorithms:

* Logic:
  * XOR all the numbers
  * XOR with all the numbers between 1 to n-1.
  * a ^ a = 0
  * 0 ^ 0 = 0
  * a ^ 0 = a
  * Complexity:
    * Time:     O(n)
    * Space:    O(1)

```python
a = [1, 2, 3, 4, 4]

xor = 0

for elem in a:
    xor = xor ^ elem
for i in range(len(a)):
    xor = xor ^ i
print(xor)
```

## REFERENCES:

<small>[500 Data Structures and Algorithms practice problems and their solutions](https://techiedelight.quora.com/500-Data-Structures-and-Algorithms-practice-problems-and-their-solutions){:target="_blank"}</small>
<small>[Find a duplicate element in a limited range array](http://www.techiedelight.com/find-duplicate-element-limited-range-array/){:target="_blank"}</small>
