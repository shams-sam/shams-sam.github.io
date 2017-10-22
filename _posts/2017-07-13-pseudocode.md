---
layout: post
title: Pseudocode
categories: []
tags: [algorithms, DSA]
description: A notation resembling a simplified programming language, used in program design
cover: "/assets/images/dsa.png"
cover_source: "https://analyticsindiamag.com/wp-content/uploads/2017/01/algoritms.png"
comments: true
---

### Pseudocode
Logic of algorithms is often expressed as pseudocode which is similar in many respects to languages like C, C++, Java etc. Major difference lies in that pseudocode uses the most **concise and meaningful** way of expressing the algorithm which can be sometimes as simple as plain english.

Also pseudocode does not get into the issues of software engineering like **abstraction, modularity or error handling**.

Pseudocode for insertion sort can be written as:

~~~
InsertionSort(A):
    for i = 1 to A.length-1
        key = A[i]
        j = i - 1
        while j > 0 and a[j] > key:
            A[j+1] = A[j]
            j--
        A[j+1] = key
~~~

### Loop Invariant and Correctness of Algorithm

A **loop invariant** is a condition [among program variables] that is necessarily true immediately before and immediately after each iteration of a loop. (Note that this says nothing about its truth or falsity part way through an iteration.)

Loop invariants are used to prove the correctness of an algorithm. There are three properties of loop invariant that must hold for the correctness of algorithm.

* **Initialization**: It is true before the first iteration of the loop.

* **Maintenance**: If it is true before an iteration of the loop, it remains true before the next iteration.

* **Termination**: It is true when the loop terminates.

Loop invariant works in a way similar to **mathematical induction**. So to prove a algorithm works, invariant must work before first iteration (**base step**), and it must hold between consecutive iterations (**inductive step**).

### General Pseudocode Conventions

* **Indentation** indicates block stucture similar to python language.
* General looping constructs used are **while**, **for**, **if-else** etc and loop counter retains its value after loop terminates.
* Variables are **local** to the given procedures.
* Parameters are **passed by value**.
* Boolean operators **and** and **or** are **short-circuiting**.



## REFERENCES:

<small>[Introduction to Algorithms 3rd Edition - Chapter 2](https://web.njit.edu/~wl256/download/cs610/Introduction-to-algorithm-3rdEdition.pdf){:target="_blank"}</small><br>
<small>[Algorithm - What is loop invariant?](https://stackoverflow.com/questions/3221577/what-is-a-loop-invariant){:target="_blank"}</small>
