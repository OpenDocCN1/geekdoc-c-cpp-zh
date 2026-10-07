
## 7.1 Introduction

Recently has been significant development in the use of nonnegative matrix factorization (NMF) for various clustering tasks. NMF factorizes an input matrix into two nonnegative matrices of lower rank. Although NMF can be used for conventional data analysis, the recent overwhelming interest in NMF is due to the newly discovered advantage of NMF to solve clustering data mining and machine learning problems. In particular, NMF with the sum of squared error cost function is equivalent to a relaxed K-means clustering, the most widely used unsupervised learning algorithm. In addition, NMF with the I-divergence cost function is equivalent to probabilistic latent semantic indexing, etc. This chapter aims to provide a comprehensive review of matrix factorization methods for clustering. We outline the theoretical foundations on NMF for clustering, provide an overview of different variants on NMF formulations, and examine several practical issues in NMF algorithms. We also summarize recent advances on use of NMF-based methods for solving many other clustering problems including co-clustering, supervised clustering, and consensus clustering and discuss some future research directions.

### 7.1.1 Background

Originally proposed for parts-of-whole interpretation of matrix factors, NMF has attracted a lot of attention and has been shown to be useful in a variety of applied settings, environments [88], chemometrics [128], pattern recognition [70], multimedia data analysis [26], text mining [130, 91], document summarization [89, 118], DNA gene expression analysis [11], financial data analysis [43], and social network analysis [128, 13, 19]. NMF can be traced back to the 1970s (Notes from [6]) and is studied extensively by Paatero and Tapper [38]. The work of Lee and Seung [67] brought much attention to NMF in machine learning and data mining fields. Algorithmic extensions of NMF have been developed to accommodate a variety of objective functions [29] and a variety of data analysis problems, including classification [71] and collaborative filtering [106]. A number of studies have focused on further computational methodologies for NMF. In addition, various extensions and variants of NMF and the complexity that NMF is NP-hard have been proposed [56, 7, 37, 39, 111, 95, 113, 38].

The true power of NMF, however, is NMF's ability to solve challenging data mining and pattern recognition problems. In fact, it has been shown [35, 37] that NMF with the sum of squared error cost function is equivalent to a relaxed K-means clustering, the most widely used unsupervised learning algorithm. In addition, NMF with the I-divergence cost function is equivalent to probabilistic latent semantic indexing, another unsupervised learning method popularly used in text analysis. Thanks to the clustering capability, NMF has attracted a lot of recent attentions in data mining.

In this chapter, we provide a comprehensive review of matrix factorization methods for clustering. To adapt to a broader audience in the data mining community, our review focuses more on conceptual foundations and interpretation rather than detailed derivations. The reader should be cautioned, however, that NMF is such a large area that truly comprehensive surveys are almost impossible, and thus, our survey may be a little eclectic. An interested reader is encouraged to consult with other papers for further reading. The reader should be cautioned also that in our presentation many mathematical descriptions are modified so that they adapt to data mining problems.

The rest of the chapter is organized as follows: the remainder of Section 7.1 introduces the basic formulations of NMF; Section 7.2 outlines the theoretical foundations on NMF for clustering and presents the equivalence results between NMF and various clustering methodologies; Section 7.3 demonstrates the NMF clustering capabilities and analyzes the advantages of NMF in clustering analysis; Section 7.4 provides an outline of the NMF algorithm development and discusses practical issues in NMF algorithms; Section 7.5 provides an overview of many different NMF variants; Section 7.6 summarizes recent advances using NMF-based methods for many other clustering problems including co-clustering, supervised clustering, and consensus clustering. Finally, Section 7.7 concludes the chapters and discusses future research directions.

### 7.1.2 NMF Formulations

Let the input data $X = (\mathbf{x}_1, \dots, \mathbf{x}_n)$ contain the collection of $n$ data column vectors. We factorize $X$ into two

$$X \approx FG^T,$$

where $X \in \mathbb{R}^{p \times n}, F \in \mathbb{R}^{p \times k}$, and $G \in \mathbb{R}^{n \times k}$. Generally, $p < n$ and the rank of $F, G$ is much lower than the rank of $X$, i.e., $k < \min(p, n)$. $F, G$ are obtained by minimizing a cost function.

$$\min_{F,G \geq 0} J_{Sse} = \|X - FG^T\|^2.$$

In this chapter, norm is implicitly assumed to be the Frobenius norm. A rank nondecreasing condition is assumed for $F, G$. Another cost function is the so-called $I$-divergence:

$$\min_{F,G \geq 0} J_{do} = \sum_{i=1}^n \left[ X_{ij} \log \frac{X_{ij}}{(FG^T)_{ij}} - X_{ij} + (FG^T)_{ij} \right].$$

It is easy to show that the inequality $I(x) \geq 0$ holds when $x=1$. The quantity $I(u,v) = u\log(u/v) - u + v$ is called $I$-divergence.

## 7.2 NMF for Clustering: Theoretical Foundations

Although NMF can be used for conventional data analysis, the overwhelming interest in NMF is due to the newly discovered advantage of NMF to solve clustering data mining and machine learning problems. Here we outline:
- (1) the relationship between NMF and K-means
- (2) the relationship between NMF and I-divergence
- (3) the relationship between NMF and spectral

### 7.2.1 NMF and K-means

The K-means algorithm is one of most used methods. Let $X = (\mathbf{x}_1, \dots, \mathbf{x}_n)$ be the data. We partition them into $K$ clusters. The K-means objective is written as:

$$J_{means} = \sum_{i=1}^n \sum_{k=1}^K h_{ik} \|\mathbf{x}_i - \mu_k\|^2,$$

where $h_{ik} = 1$ if $\mathbf{x}_i$ belongs to cluster $k$, and $0$ otherwise. $\mu_k$ is the centroid of cluster $k$. This can be rewritten as:

$$J_{means} = \sum_{i=1}^n \|\mathbf{x}_i - \sum_{k=1}^K h_{ik} \mu_k\|^2.$$

### 7.2.2 NMF and Probabilistic Semantic Indexing

Probabilistic Latent Semantic Indexing (PLSI) is an unsupervised learning method based on statistical models and has been successfully applied to document clustering. PLSI maximizes the likelihood:

$$J_{PLSI} = \sum_{i=1}^n \sum_{j=1}^m X_{ij} \log P(w_i, d_j),$$

where the joint occurrence probability is factorized:

$$P(w_i, d_j) = \sum_{k} P(w_i|z_k)P(d_j|z_k)P(z_k),$$

assuming that $w_i$ and $d_j$ are conditionally independent given $z_k$.

Theorem 2 PLSI is identical to NMF with I-divergence.
(A) The objective function of PLSI is identical to the objective function of NMF using I-divergence.
(B) We can express $FG^T = F\hat{D}G^T$ where $F,\hat{D},G^T$ satisfy the probability normalization: $\sum_{i=1}^n F_{ik}=1, \sum_{j=1}^m G_{jk}=1, \sum_{k=1}^k \hat{D}_{kk}=1$.

### 7.2.3 NMF and Kernel K-means for Spectral Clustering

For a square symmetric matrix $W$, we would expect a $W \approx HH^T$ decomposition. The following theorem points out its usefulness for document clustering:

Theorem 3 Orthogonal symmetric NMF
$$\min_{H\geq 0} \|W - HH^T\|^2, \text{s.t.} } H^T H = I.$$

is equivalent to kernel K-means clustering.
