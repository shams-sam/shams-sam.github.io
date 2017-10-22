---
layout: post
title: Insertion Sort
categories: []
tags: [algorithms, DSA]
description: The simplest sorting algorithm that works the way one would sort playing cards in hand.
cover: "/assets/images/dsa.png"
cover_source: "https://analyticsindiamag.com/wp-content/uploads/2017/01/algoritms.png"
comments: true
mathjax: true
---

### Insertion Sort
Given an array A[1...n] of length n to be sorted. The algorithm sorts the list **inplace**. It picks an element i as **key** and places it in the correct position in the sorted A[1..(i-1)].

![Insert Sort Visualization](/assets/2017-07-13-insertion-sort/fig-1-insertion-sort.png?raw=true)

Time Complexity: \\(O(n^2)\\)

Space Complexity: \\(O(n)\\)

### Pseudocode

```
InsertionSort(A):
    for i = 1 to A.length-1
        key = A[i]
        j = i - 1
        while j > 0 and a[j] > key:
            A[j+1] = A[j]
            j--
        A[j+1] = key
```

### Java Code

```java
public class InsertionSort {
    
    public int[] insertionSort(int[] arr) {
        
        int length = arr.length;
        int key, j, i;
        for(j = 1; j < length; j++) {
            key = arr[j];
            i = j-1;
            while(i >= 0 && arr[i] > key) {
                arr[i+1] = arr[i];
                i--;
            }
            arr[i+1] = key;
        }
        
        return arr;
        
    }
    
    public static void print_arr(int[] arr) {
        
        for(int i: arr) {
            System.out.printf("%d ", i);
        }
        
    }

    public static void main(String[] args) {
        
        InsertionSort i = new InsertionSort();
        int[] arr = {9, 8, 7, 6, 5};
        int[] sorted = i.insertionSort(arr);
        InsertionSort.print_arr(sorted);

    }

}
```

## REFERENCES:

<small>[Introduction to Algorithms 3rd Edition - Chapter 2](https://web.njit.edu/~wl256/download/cs610/Introduction-to-algorithm-3rdEdition.pdf){:target="_blank"}</small>