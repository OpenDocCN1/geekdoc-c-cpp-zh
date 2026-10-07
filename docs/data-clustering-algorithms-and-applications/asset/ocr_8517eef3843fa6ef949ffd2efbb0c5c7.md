# Alternative Clustering Analysis: A Review

```
$I(C_1;C_2) = \sum_{C_1} \sum_{C_2} (p(C_1,C_2) - p(C_1)p(C_2))^2$
```

When $\eta$ is a regularization parameter, $p(\cdot)$ is the probability density, and the mutual information $I(C_1;C_2)$ is in a quadratic form of the mutual information, which has the advantage of amenable to density estimation using a Parzen window technique with Gaussian Kernel. This objective can then be used as a component in a hierarchical clustering framework to generate an alternative clustering. To use NACI, choices must be made for both the regularization parameter and the kernel parameter.

Another approach in the same spirit as NACI is that of minEntropy [27], instead of using a hierarchical algorithm with the quadratic mutual information, uses a $k$-means style algorithm with quadratic mutual information. The style is again sequential and requires specification of a kernel width and tradeoff parameter.

# 21.3.5.4 mSC

The final method in this section is the mSC alternative clustering approach outlined in [28]. This is a spectral approach that can simultaneously generate multiple alternative clusters.

Rather than being on mutual information, it uses the Hilbert-Schmidt Independence Criterion (HSIC) to assess the correlation between clusters. With mutual information, the HSIC is also able to recognize nonlinear dependencies. Specifically, the mSC technique embeds the HSIC measure within a spectral clustering framework. The objective is a dual function, where each iteration, one term is fixed and the other is optimized. The user is able to specify the number of alternative clusters that are desired and the number of clusters in each.

# 21.4 Connections to Multiview Clustering and Subspace Clustering

We have far reviewed a range of techniques that can be used for generating alternative clusters, which is a core component for multiple clustering analysis. We now mention the connections that exist between alternative clustering analysis and other directions: multiview clustering and subspace clustering.

Multiview clustering is also considered with multiple clustering, but from a different angle. In multiview clustering, one is provided with multiple sources or representations of data (multiple views) and wishes to learn a single clustering which is both consistent with a good reflection of the multiple views. A prototypical example is Web pages, which may be modeled using features which describe the frequencies of words occurring in the page (View 2), or modeled using features which describe the anchor text in the links going out of the page (View 3). It has been found that using the information in all views simultaneously, one can generate a better clustering than using only a single view obtained by merging the features. A particular benefit of multiview clustering is that using multiple views to produce a clustering can reduce the effect of noise within individual views. If one were to use a single view to drive the clustering, the presence of noise might corrupt the clusters and make the detection of cluster structure more difficult. Using multiple views to cluster, however, lessens the likelihood of noise within a view being dominant and emphasizes their contribution toward the overall cluster structure.