---
layout: post
title: Divide and Conquer
categories: []
tags: [algorithms, DSA]
description: Divide and conquer is an algorithm design paradigm based on multi-branched recursion
cover: "/assets/images/dsa.png"
cover_source: "https://analyticsindiamag.com/wp-content/uploads/2017/01/algoritms.png"
comments: true
---

### Recursion
The process in which a function calls itself directly or indirectly is called recursion and the corresponding function is called as **recursive function**.

* **Base Condition**: In a recursive problem, solution to the base case is provided and solution to bigger problem is expressed in terms of smaller problems.
* **Stack Overflow**: In a recursion if the base condition is not reached and the function call stack reaches its limit, a stack overflow error is thrown.
* **Direct vs Indirect Recursion**: A function is **direct recursive** if it calls the same function, but a **indirect recursive** function calls a different method which inturn calls the original function.
* **Tail Recursion**: If the recursive call is the last thing executed by the function.
* **Disadvantage**: Greater space requirements and additional overhead for function calls and return values.

### Divide and Conquer Approach
The divide and conquer paradigm involves three steps:

* **Divide**: Divide a problem into a number of smaller subproblems.
* **Conquer**: Solve the subproblems recursively.
* **Combine**: Combine solution to subproblems to get the solution of original problem.

For example **merge sort** is based on divide and conquer paradigm. It follows the following steps:

* Divide array of size n to be sorted into two of size n/2.
* Sort the sub-arrays recursively.
* Combine the two sorted sub-arrays to get the sorted array.

Base case is when the sub-array has only a single element and is trivially sorted.

Auxiliary procedure Merge(A, p, q, r) where A is the array and p, q and r are indices into the array such that p <= q <= r.

Merge procedure assumes that the sequence A[p .. q] and A[q+1 .. r] are in sorted order and return A[p .. r] in sorted order. 

**Time Complexity of the Merge(A, p, q, r) procedure is O(n)**.

## REFERENCES:

<small>[Introduction to Algorithms 3rd Edition - Chapter 2](https://web.njit.edu/~wl256/download/cs610/Introduction-to-algorithm-3rdEdition.pdf){:target="_blank"}</small><br>
<small>[Recursion - GeeksforGeeks](http://www.geeksforgeeks.org/recursion/){:target="_blank"}</small>