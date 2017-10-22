---
layout: post
title: Linear Algebra Review
categories: []
tags: [machine learning, mathematics, andrew ng]
description: Linear algebra is the branch of mathematics concerning vector spaces and linear mappings between such spaces
cover: "/assets/images/linear-algebra.png"
cover_source: "https://ka-perseus-images.s3.amazonaws.com/6eca6b57567643dd7743f2efc5c90e6bad3133d8.png"
comments: true
mathjax: true
---

### Matrices
In mathematics, a matrix is a **rectangular array** of numbers, symbols, or expressions, arranged in rows and columns. For example, A is a matrix below, 

$$ A = 
  \begin{bmatrix}
    123 & 23 & 324 \\
    12 & 231 & 42 \\
  \end{bmatrix}
$$

**Dimension** of a matrix is given by n * m where **n is number of rows** and **m is number of columns**. So the matrix above is a 2*3 matrix. It is also sometimes represented as \\(\mathbb{R}^{2\*3}\\).

Matrices are generally represented with **uppercase**. Also, if A is a matrix, \\(A_{ij}\\) is the **i,j entry** i.e. the element in \\(i^{th}\\) row and \\(j^{th}\\) column. For example, 

$$A_{23} = 42$$

### Vectors
In mathematics, vector is a matrix that has **only one column**. For example, x is a vector below,

$$ x = 
  \begin{bmatrix}
    12 \\
    1 \\
    124 \\
  \end{bmatrix}
$$

So effectively vector is a n * 1 matrix where **n is the number of rows**. It is termed as **n-dimensional vector**. It is also sometimes represented as \\(\mathbb{R}^n\\).

Vectors are generally represented with **lowercase**. Also, if x is a matrix, \\(x_{i}\\) is the element in \\(i^{th}\\) row. For example, 

$$x_2 = 1$$

Vectors can be **0 or 1 indexed** i.e. the start of index numbering may begin with 0 or 1. Generally in mathematics, 1-indexed notation is followed while in computer science 0-indexed notation is more popular.

### Matrix Addition

* Matrix addition is nothing but adding them element by element. 
* Only matrices of same dimensions can be added
* The **resultant matrix has same dimension**. 
* The operation is commutative, associative and distributive.

For example,

$$
  \begin{bmatrix}
    1 & 2 \\
    3 & 4 \\
  \end{bmatrix} +
  \begin{bmatrix}
    3 & 2 \\
    6 & 1 \\
  \end{bmatrix} = 
  \begin{bmatrix}
    4 & 4 \\
    9 & 5 \\
  \end{bmatrix}
$$

### Scalar Multiplication

* Scalar multiplication is multiplication of a real number with each element of the matrix. 
* **The resultant matrix has the same dimension.** 
* The operation is commutative, associative and distributive.

For example,

$$
  3 *
  \begin{bmatrix}
    3 & 2 \\
    6 & 1 \\
  \end{bmatrix} = 
  \begin{bmatrix}
    9 & 6 \\
    18 & 3 \\
  \end{bmatrix}
$$

$$
  \begin{bmatrix}
    4 & 2 \\
    6 & 8 \\
  \end{bmatrix} / 2 = 
  \begin{bmatrix}
    2 & 1 \\
    3 & 4 \\
  \end{bmatrix}
$$

> Matrix operation follow the BODMAS rule for the order of precedence.

### Matrix Vector Multiplication
Consider matrix A and vector x, then the matrix-vector multiplication is given by,

$$
  \begin{bmatrix}
    a_{11} & a_{12} & \cdots & a_{1n} \\
    a_{21} & a_{22} & \cdots & a_{2n} \\
    \vdots & \vdots & \ddots & \vdots \\
    a_{m1} & a_{m2} & \cdots & a_{mn} \\
  \end{bmatrix}
  \begin{bmatrix}
    x_1 \\
    x_2 \\
    \vdots \\
    x_n
  \end{bmatrix} 
  = 
  \begin{bmatrix}
    a_{11}*x_1 + a_{12}*x_2 + \cdots + a_{1n}*x_n \\
    a_{21}*x_1 + a_{22}*x_2 + \cdots + a_{2n}*x_n \\
    \vdots \\
    a_{m1}*x_1 + a_{m2}*x_2 + \cdots + a_{mn}*x_n \\
  \end{bmatrix}
$$

Following properties are inferred:

* **Operation is not always commutative**.
* Number of columns in matrix A has to match the number of rows in vector x.
* The resultant vector of the multiplication is of dimension n as can be seen above. So if A is m*n and x is n-dimensional then, resultant is m-dimensional vector.

**Application**
A hypothesis \\(h_\theta(x) = -40 + 0.25\,x\\) can be applied to a set of x's such as (2104, 1416, 1534, 852) then it can be done as follows,

$$
  \begin{bmatrix}
    1 & 2104 \\
    1 & 1416 \\
    1 & 1534 \\
    1 & 852 \\
  \end{bmatrix}
  *
  \begin{bmatrix}
    -40 \\ 
    0.25 \\
  \end{bmatrix}
  =
  \begin{bmatrix}
    486 \\
    314 \\ 
    344 \\
    173 \\
  \end{bmatrix}
$$


### Matrix-Matrix Multiplication
It is a binary operation that produces a matrix from two matrices. So, if A is \\(n * m\\) matrix and B is a \\(m * p\\) matrix, then their product AB is a \\(n * p\\) matrix. The m enteries along rows of A are multiplied with the m enteries along the column of B and summed to produce elements of AB. **When two linear transformations are represented by matrices, then the matrix product represents the composition of the two transformations.**

$$
  \begin{bmatrix}
    a_{11} & a_{12} & \cdots & a_{1m} \\
    a_{21} & a_{22} & \cdots & a_{2m} \\
    \vdots & \vdots & \ddots & \vdots \\
    a_{n1} & a_{n2} & \cdots & a_{nm} \\
  \end{bmatrix}
  \begin{bmatrix}
    b_{11} & b_{12} & \cdots & b_{1p} \\
    b_{21} & b_{22} & \cdots & b_{2p} \\
    \vdots & \vdots & \ddots & \vdots \\
    b_{m1} & b_{m2} & \cdots & b_{mp} \\
  \end{bmatrix}
  = 
  \begin{bmatrix}
    (AB)_{11} & \cdots & (AB)_{1p} \\
    (AB)_{21} & \cdots & (AB)_{2p} \\
    \vdots & \ddots & \vdots \\
    (AB)_{n1} & \cdots & (AB)_{np} \\
  \end{bmatrix}
$$

Following properties are inferred:

* **Operation is not always commutative**.
* Number of columns in matrix A has to match the number of rows in vector x.

**Application**
Consider three hypothesis as follows,

$$h_\theta(x) = -40 + 0.25\,x$$

$$h_\theta(x) = 200 + 0.1\,x$$

$$h_\theta(x) = -150 + 0.4\,x$$

All three can be applied to a set of inputs as shown in matrix-vector multiplication.

$$
  \begin{bmatrix}
    1 & 2104 \\
    1 & 1416 \\
    1 & 1534 \\
    1 & 852 \\
  \end{bmatrix}
  *
  \begin{bmatrix}
    -40 & 200 & -150 \\ 
    0.25 & 0.1 & 0.4\\
  \end{bmatrix}
  =
  \begin{bmatrix}
    486 & 410 & 692 \\
    314 & 342 & 416 \\ 
    344 & 353 & 464 \\
    173 & 285 & 191 \\
  \end{bmatrix}
$$

Here, each column corresponds to a specific hypothesis.

### Matrix Multiplication Properties

* **Commutative Property**: Scalar multiplication is commutative while matrix multiplication is not commutative.
* **Associative Property**: Scalar and matrix multiplication are both associative.
* **Identity Matrix**: Denoted by I (or \\(I_{n*n}\\)) has all elements zero except for the main diagonal elements which are set to 1. It has the following properties.

$$A \cdot I = I \cdot A = A$$

### Inverse
In the space of real numbers each number is said to have an inverse if the product of the number and the inverse results in the identity i.e. 1. Also not all the real numbers have an inverse, for example, the number 0 does not have an inverse, because 1/0 is undefined.

Similarly, a matrix A is said to have an inverse if there exists a \\(A^{-1}\\) such that

$$A(A^{-1}) = (A^{-1})A = I$$

> Only square matrices have inverses.

> Matrices that do not have an inverse are called singular or degenerate matrices.

### Transpose

Given a matrix A, having dimension m * n and let \\(B = A^T\\) be its transpose, then B is a n * m matrix such that,

$$B_{ij} = A_{ji}$$

It is basically the operation where each row is sequentially replaced as a column in the resultant matrix.

## REFERENCES:

<small>[Machine Learning: Coursera - Matrices and Vectors](https://www.coursera.org/learn/machine-learning/lecture/38jIT/matrices-and-vectors){:target="_blank"}</small><br>
<small>[Machine Learning: Coursera - Addition and Scalar Multiplication](https://www.coursera.org/learn/machine-learning/lecture/R4hiJ/addition-and-scalar-multiplication){:target="_blank"}</small><br>
<small>[Machine Learning: Coursera - Matrix Vector Multiplication](https://www.coursera.org/learn/machine-learning/lecture/aQDta/matrix-vector-multiplication){:target="_blank"}</small><br>
<small>[Machine Learning: Coursera - Matrix Matrix Multiplication](https://www.coursera.org/learn/machine-learning/lecture/dpF1j/matrix-matrix-multiplication){:target="_blank"}</small><br>
<small>[Machine Learning: Coursera - Matrix Multiplication Properties](https://www.coursera.org/learn/machine-learning/lecture/W1LNU/matrix-multiplication-properties){:target="_blank"}</small><br>
<small>[Machine Learning: Coursera - Inverse and Transpose](https://www.coursera.org/learn/machine-learning/lecture/FuSWY/inverse-and-transpose){:target="_blank"}</small><br>
<small>[Matrix Multiplication: Wikipedia](https://en.wikipedia.org/wiki/Matrix_multiplication){:target="_blank"}</small>
