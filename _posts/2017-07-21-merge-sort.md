---
layout: post
title: Merge Sort
categories: []
tags: [algorithms, DSA]
description: Merge Sort is a Divide and Conquer algorithm. It divides input array in two halves, calls itself for the two halves and then merges the two sorted halves.
cover: "/assets/images/dsa.png"
cover_source: "https://analyticsindiamag.com/wp-content/uploads/2017/01/algoritms.png"
comments: true
mathjax: true
---

### [Merge Sort](https://en.wikipedia.org/wiki/Merge_sort){:target="_blank"}
Merge sort is an efficient, general-purpose, comparison-based sorting algorithm. Most implementations produce a stable sort, which means that the implementation preserves the input order of equal elements in the sorted output. Merge sort is a **divide and conquer** algorithm that was invented by John von Neumann in 1945.

Time Complexity: \\(O(n\,log\,n)\\)

### Pseudocode

~~~
Merge(A, p, q, r):
  n1 = p - q + 1
  n2 = r - q
  L = arr[n1]
  R = arr[n2]
  for k = 1 to n1:
    L[k] = A[p + k - 1]
  for k = 1 to n2:
    R[k] = A[q + k]
  i = 1
  j = 1
  for k = p to r:
    if L[i] <= R[j]:
      A[k] = L[i]
      i++
    else 
      A[k] = R[j]
      j++
~~~

### Java Code

~~~java

public class MergeSort {
    
    public static int[] merge(int[] arr_l, int[] arr_r) {
        
        int[] arr = new int[arr_l.length + arr_r.length];
        int k;
        int l = 0;
        int r = 0;
        for(k = 0; k < arr.length; k++) {
            if(arr_l[l] <= arr_r[r]) {
                arr[k] = arr_l[l];
                l++;
            } else {
                arr[k] = arr_r[r];
                r++;
            }
            if(l==arr_l.length || r==arr_r.length) {
                k++;
                break;
            }
        }
        
        for(int j = l; j < arr_l.length; j++) {
            arr[k] = arr_l[j];
            k++;
        }
        for(int j = r; j < arr_r.length; j++) {
            arr[k] = arr_r[j];
            k++;
        }
        
        return arr;
        
    }
    
    public static int[] merge_sort(int[] arr) {
        
        if(arr.length == 1) return arr;
        
        int mid = (int) arr.length/2;
        
        int left = mid;
        int[] arr_l = new int[left];
        for(int k = 0; k < left; k++) arr_l[k] = arr[k];
        
        int right = arr.length-mid;
        int[] arr_r = new int[right];
        for(int k = 0; k < right; k++) arr_r[k] = arr[mid+k];
        
        arr_l = merge_sort(arr_l);
        arr_r = merge_sort(arr_r);
        arr = merge(arr_l, arr_r);
        
        return arr;
        
    }
    
    public static void print_arr(int[] arr) {
        
        for(int i: arr) {
            System.out.printf("%d ", i);
        }
        System.out.println("\n");
        
    }

    public static void main(String[] args) {

        int[] arr = {1, 9, 8, 7, 6, 10, 5, 9};
        MergeSort.print_arr(MergeSort.merge_sort(arr));

    }

}

~~~

### Java Code for Inplace Merge Sort

~~~java

public class MergeSortInplace {
    
    static int[] arr;
    
    public static void merge(int start, int mid, int end) {
        
        int[] aux_arr = new int[end-start+1];
        int k;
        
        for(k = 0; k < end-start+1; k++) {
            aux_arr[k] = arr[start + k];
        }
        
        k=start;
        int i = 0;
        int j = mid-start+1;
        
        while(i <= mid-start && j <= end-start) {
            if(aux_arr[i] <= aux_arr[j]) {
                arr[k] = aux_arr[i];
                i++;
            } else {
                arr[k] = aux_arr[j];
                j++;
            }
            k++;
        }
        
        while(i<= mid-start) {
            arr[k] = aux_arr[i];
            i++;
            k++;
        }
        
        while(j<=end-start) {
            arr[k] = aux_arr[j];
            j++;
            k++;
        }
        
    }
    
    public static void merge_sort(int start, int end) {
        
        if(start >= end) return;
        int mid = start + (end-start)/2;
        merge_sort(start, mid);
        merge_sort(mid+1, end);
        merge(start, mid, end);
        
    }
    
    public static void print_arr(int[] arr) {
        
        for(int i: arr) System.out.printf("%d ", i);
        System.out.println();
        
    }

    public static void main(String[] args) {
        
        int[] arr = {1, 3, 2, 5, 4, 7, 6, 10, 5, 8, 9};
        MergeSortInplace.arr = arr;
        merge_sort(0, MergeSortInplace.arr.length-1);
        print_arr(MergeSortInplace.arr);

    }

}

~~~

## REFERENCES:

<small>[Introduction to Algorithms 3rd Edition - Chapter 2](https://web.njit.edu/~wl256/download/cs610/Introduction-to-algorithm-3rdEdition.pdf){:target="_blank"}</small><br>
<small>[Merge Sort - Wikipedia](https://en.wikipedia.org/wiki/Merge_sort){:target="_blank"}</small>
