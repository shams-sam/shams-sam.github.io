---
layout: post
title: Sort Binary Array
categories: []
tags: [array algorithms, references, algorithms]
cover: "/assets/images/algorithm.png"
cover_source: "https://www.pixelstalk.net/mathematics-hd-desktop-wallpapers/"
description: To sort a binary array using Quicksort logic.
comments: true
---

### Q: Sort a given binary array.

#### Input:

```python
a = [1, 0, 1, 0, 1, 0, 0, 1]
```

#### Output:

```python
[0, 0, 0, 0, 1, 1, 1, 1]
```

#### Algorithms:

* Logic:
  * Iterate and fill available position with 0 if 0 found in list.
  * Fill remaining positions with 1s.
  * Complexity:
    * Time:     O(n)
    * Space:    O(1)

```python
a = [1, 0, 1, 0, 1, 0, 0, 1]

k = 0 

for i in a:
    if i==0:
        a[k] = 0
        k += 1
for i in range(k, len(a)):
    a[i] = 1
```

* **Quicksort** Logic:
  * Complexity:
    * Time:     O(n)
    * Space:    O(1)

```python
a = [1, 0, 1, 0, 1, 0, 0, 1]

pivot = 1
start = 0
end = len(a) - 1
j = 0

while start < end:   
    if a[j] < pivot:
        a[j], a[start] = a[start], a[j]
        start += 1
        j += 1
    elif a[j] >= pivot:
        a[j], a[end] = a[end], a[j]
        end -= 1
```

## REFERENCES:

<small>[500 Data Structures and Algorithms practice problems and their solutions](https://techiedelight.quora.com/500-Data-Structures-and-Algorithms-practice-problems-and-their-solutions){:target="_blank"}</small>
<small>[Sort binary array in linear time](http://www.techiedelight.com/sort-binary-array-linear-time/){:target="_blank"}</small>
