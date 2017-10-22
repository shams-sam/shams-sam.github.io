---
layout: post
title: Random Projection in Dimensionality Reduction
categories: []
tags: [concept, machine learning, mathematics]
description: The dimensions and distribution of random projections matrices are controlled so as to preserve the pairwise distances between any two samples of the dataset.
cover: "/assets/images/projection.jpg"
cover_source: "https://upload.wikimedia.org/wikipedia/commons/thumb/4/4f/Staircase_perspective.jpg/1200px-Staircase_perspective.jpg"
comments: true
mathjax: true
---

### Introduction
Random Projections have emerged as a powerful method for dimensionality reduction. Theoretical results indicate that it **preserves distances** quite nicely but empirical results are **sparse**. It is often employed in dimensionality reduction in both **noisy and noiseless data** especially image and text data. Results of projecting on **random lower-dimensional subspace** yields results comparable to conventional methods like PCA etc but using it is **computationally less expensive** than the traditional alternatives.

### Curse of Dimensionality

* High dimensional data **restricts the choice** of data processing methods.
* A statistically optimal way of dimensionality reduction is to project the data onto a lower-dimensional orthogonal subspace that **captures as much of the variations of the data as possible**. The most widely used method of this sort is PCA (**Principal Component Analysis**).
* Drawback of PCA is however that it is **computationally expensive** to calculate as the dimensions of data increases.

### Johnson-Lindenstrauss Lemma

**If points in vector space are projected onto a randomly selected subspace of suitably high dimensions, then the distances between the points are approximately preserved.**

### Random Projection (RP)

* In RP, a higher dimensional data is projected onto a lower-dimensional subspace **using a random matrix whose columns have unit length**.
* RP is computationally efficient, yet accurate enough for this purpose as it does not introduce a significant distortion in the data.
* It is not sensitive to impulse noise. So RP is promising alternative to some existing methods in **noise reduction** (like mean filtering) too.

* The original d-dimensional data is projected to a k-dimensional \\((k \lt \lt d)\\) through the origin, using a random \\(k * d\\) matrix R whose columns have unit lengths. It is given by

$$X_{k*N}^{RP} = R_{k*d} \, X_{d*N} \tag{1}$$

  * Where 
    * \\(X_{k*N}^{RP}\\) is the k-dimensional random projection
    * \\(R_{k*d}\\) is the random matrix used for transformation
    * \\(X_{d*N}\\) are the original set of N d-dimensional observations

* The key idea of random mapping arises from **Johnson-Lindenstrauss Lemma**

* **Complexity**
  * Forming a random matrix R and projecting d * N data matrix X into k dimensions is of the order **O(dkN)**
  * If X is a sparse matrix with c non-zero values per column, then the complexity is **O(ckN)**

* Theoretically, equation (1) is not a projection because R is generally not orthogonal. A linear mapping like (1) can cause significant distortion in data if R is not orthogonal. **Orthogonalizing R is computationally expensive.**

* Instead of orthogonalizing, RP relies on the result presented by Hecht-Neilsen i.e. **In a high dimensional space, there exists a much larger number of almost orthogonal than orthogonal directions.** Thus the vectors with random directions might be sufficiently close to orthogonal, and equivalently \\(R^TR\\) would approximate an identity matrix.

* Experimental results show the mean squared difference between \\(R^TR\\) and identity matrix is around **1/k per element**.

* Euclidean distances between \\(x_1\\) and \\(x_2\\) in the original large-dimensional space is given by

$$||x_1 - x_2||$$

* After RP, this distance can be approximated by **scaled Euclidean distance** of these vectors in reduced spaces:

$$\sqrt{d \over k} || Rx_1 - Rx_2 ||$$

  * Where d is the original and k is the reduced dimensionality of the data set and **scaling factor** \\(\sqrt{d \over k}\\) takes into account the decrease in dimensionality of the data set.

* According to **Johnson-Lindenstrauss Lemma**, the expected norm of a projection of unit vector onto a random subspace through origin is \\(\sqrt{k \over d}\\).

* The choice of R matrix is generally such that \\(r_{ij}\\) of R are often **Gaussian Distributed** although many other choices are available. There is a peculiar result which says one can use the following distribution which is much simpler.

$$
  \begin{equation}
    X= \sqrt{3} * 
    \begin{cases}
      +1 & \text{ with probability }\ {1\over6} \\
      0 & \text{ with probability }\ {2\over3} \\
      -1 & \text{ with probability }\ {1\over6}
    \end{cases}
    \tag{2}
  \end{equation}
$$

* Practically, all zero mean, unit variance distributions of \\(r_{ij}\\) would give a mapping that satisfies the Johnson-Lindenstrauss Lemma.

* Equation (2) helps reduce the computational expense even further.

### Principal Component Analysis (PCA)

* PCA is eigenvalue decomposition of the data covariance matrix. It is computed as 

$$E\{XX^T\} = E \Lambda E^T$$
 
  * Where
    * columns of E are the eigenvectors of the data covariance matrix \\(E\{XX^T\}\\)
    * \\(\Lambda\\) is a the diagonal matrix containing the respective eigenvalues.

* Dimensionality reduction of data set is obtained by projection on a subspace spanned by most important eigenvectors, given by

$$X^{PCA} = E_k^T X$$

  * Where
    * The d * k matrix \\(E_k\\) contains the k eigenvectors corresponding to the k larges eigenvalues.

* PCA is the optimal way to project data in the mean-square sense, i.e. the squared error introduced in the projection is minimized over all projections onto a k-dimensional space.

* Eigen value decomposition of the data covariance matrix is very expensive. 

* **Computational Complexity** : \\(O(d^2N) + O(d^3)\\)

### Singular Value Decomposition (SVD)

* Closely related to PCA, singular value decomposition is given by

$$X = USV^T$$

  * Where 
    * Orthogonal matrices U and V contain the left and right singular vectors of X respectively
    * The diagonal matrix S contains the singular values of X.

* Using SVD, the dimensionality of data can be reduced by projecting data onto the space spanned by the left singular vectors corresponding to the k largest singular values, given by 

$$X^{SVD} = U_k^T X$$

  * Where \\(U_k\\) is of size d * k and contains k singular vectors.

* Like PCA, SVD is also expensive to compute.

* For sparse data matrix \\(X_{d*N}\\) with about c non-zero entries per column, the **computational complexity** is of the order **O(dcN)**.

### Latent Semantic Indexing (LSI)

* It is a dimensionality reduction method for text document data.

* Using LSI, the document data is represented in a **lower-dimensional "topic" space: the documents are characterized by some underlying (latent, hidden) concepts referred to by the terms**.

* LSI can be computed either by PCA or SVD of the data matrix of N d-dimensional document vectors.

### Discrete Cosine Transform (DCT)

* Widely used for image compression and can be used for dimensionality reduction of image data.

* Computational more efficient than PCA and has performance approachable to PCA.

* DCT is optimal for human eye: **the distortions introduced occur at the highest frequencies only**, neglected by human eye as noise.

* DCT can be performed by simple matrix operations: **Image is first transformed to DCT space and dimensionality reduction is achieved during inverse transform by discarding the transform coefficients corresponding to highest frequencies.**

* Computing DCT is **not data-dependent**, unlike PCA that needs the eigenvalue decomposition of data covariance matrix, which is why DCT is orders of magnitude cheaper to compute than PCA.

* **Computational Complexity** : \\(O(dN\,log_2(dN))\\) for data matrix of size d * N.

### Notes About Random Projection

* RP does not distort the data significantly more than PCA. Also at smaller dimensions PCA seems to distort data more than RP because of removal of significantly important eigenvectors by elimination.

* Computational complexity of RP is significantly lesser than other methods like PCA, but more than DCT.

* So it can be inferred that **RP are a better choice given the trade off of DCT accuracy for reduced complexity**.

* **At smaller dimension RP outperforms DCT both on accuracy and complexity**.

* Use case can often be a factor in considering the most optimal way of dimensionality reduction. Say, even though RP outperforms DCT, it cannot be used for purposes where aim is to transmit the minimized dataset and re-obtain original data on the other end for human viewing. 

* **Psuedoinverse computation of R is expensive** to compute but because R is almost orthogonal, \\(R^T\\) would be a **good approximation of psuedoinverse**. So the image can be computed from RP as, 

$$X_{d*N}^{new} = R_{d*k}^T X_{k*N}^{RP}$$

  * Where \\(X_{k*N}^{RP}\\) is the result of random projection. But the **obtained image is visually worse than a DCT compressed image**, to a human eye.

* So RP would serve very well in applications where distance or similarity between data vectors should be preseved under dimensionality reduction as well as possible, but where data is not intended to be visualized for the human eye, eg. machine vision.

* In case of text dataset, the error in dimensionality reduction is calculated by calculating the **inner product among randomly chosen data pairs before and after transform**. It is observed that RP is not as accurate as SVD but the error may be neglectable in various use cases. The possible cause could be that the Johnson-Lindenstrauss makes statement about Euclidean distance, but **Inner product is a different metric even if Euclidean distance is maintained well**.

## REFERENCES

<small>[Random projection in dimensionality reduction: Applications to image and text data](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.24.5135&rep=rep1&type=pdf){:target="_blank"}</small><br>
<small>[Various Embeddings on Digits Data - Python Sklearn](http://scikit-learn.org/stable/auto_examples/manifold/plot_lle_digits.html#sphx-glr-auto-examples-manifold-plot-lle-digits-py){:target="_blank"}</small>