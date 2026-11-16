
## Clustering

Clustering is introduced as a sorting process where the criteria governing the sort are not known. It builds from the heuristic K means clustering, explaining mixture models in general and specifically Gaussian mixture models. The Expectation-Maximization technique is shown to be a general iterative technique to maximize the data likelihood. Next Bayesian mixture models are explored and illustrated with the Chinese Restaurant Process. The chapter concludes with the Dirichlet process which is explained in detail and illustrated by examples.

So far we have looked at data which had class labels. The task was to learn the class membership from the features of each data sample, in order to classify unseen data in the future. In this chapter, we look at unlabeled data. As before, we denote the vector of features by v. Let v1, ..., vN be the feature vectors of N data samples. The choice of features or combination of features is important.

![](img/d3c00252180686426c9e63ab889b535b_169_0.png)

Figure 6.1: Sorting sweets.

For example, a popular exercise for children to apply their observation and sorting skills is to let them sort sweets. It is immediately obvious that there are numerous distinguishing features. Firstly, there is the size, then the colour, or the sweet might be multicoloured. They come in all sorts of shapes. Next, we might consider the main ingredient which may be chocolate, jelly, liquorice or something completely different, or it might be a combination of different ingredients, or have a filling. The parents might be more interested in keeping the overall sugar intake low, while a dentist might be interested in whether the sweets stick to the teeth or not. Depending on their tastes and preferences, different people will put different emphasis on each feature.

Clustering often is the first step when analysing a new data set. If not much is known yet about the data, it is useful to see whether the data separates naturally into different groups. The aim is to find clusters where data samples within one cluster are more similar to each other than to data samples in other clusters. We will see in the following what similar means for different algorithms.

There are many application areas. For example, clustering is used to find news articles with similar contents or relating to the same topic. Similarly, search engines use clustering algorithms. The suggestions we receive on streaming sites depending on our past preferences are based on clusters as well. Image segmentation is another application area is lossy data compression, where it is sufficient to represent the data by the cluster it belongs to. It is also used in bioinformatics to analyze biological data of all sorts.

### 6.1 K Means Clustering

K means clustering decides at the outset on the numbers of clusters denoted by $K$ and each data sample is assigned to exactly one cluster. This is known as hard clustering. The aim is to find cluster centres $\mu_1, \dots, \mu_K$ such that the sum of the squared distances of each data sample to its nearest cluster centre (the one it is assigned to) is minimal. Nearest here is with respect to the Euclidean norm ($L_2$ norm). Thus the objective function is

\( J = \sum_{n=1}^N \min_k \| \mathbf{v}_n - \mu_k \|^2. \)

This optimization problem is NP hard. That is, there is no known algorithm to solve this in polynomial time. This is because as cluster centres move around, for each sample it changes which is the nearest cluster. The algorithm finds an approximate solution by separating this interdependency with the introduction of hidden (latent) variables $\mathbf{z}_n$, one for each data sample $\mathbf{v}_n$. The latent variables are binary variables, i.e. $\mathbf{z}_n \in \{0, 1\}^K$, where only one entry can be 1 and the others have to be 0. This is known as a 1-of-K representation. A 1 in the \(k^{th}\) entry indicates that $\mu_k$ is the nearest cluster centre to $\mathbf{v}_n$. Let \(z_{n,k}\) be the \( k^{\text{th}} \) component of \( \mathbf{z}_n \). The objective function can then be rewritten as

\( J = \sum_{n=1}^N \sum_{k=1}^K z_{n,k} \| \mathbf{v}_n - \boldsymbol{\mu}_k \|^2 \).

This is quadratic in \( \boldsymbol{\mu}_k \). The minimum is found by differentiating with respect to \( \boldsymbol{\mu}_k \) for each \( k \) using Appendices A.2.1 and A.2.2 and setting this to zero,

\( 2 \sum_{n=1}^N z_{n,k} (\mathbf{v}_n - \boldsymbol{\mu}_k) = 0 \).

This gives new centre locations for all \( k \)

\( \boldsymbol{\mu}_k = \frac{\sum_{n=1}^N z_{n,k} \mathbf{v}_n}{\sum_{n=1}^N z_{n,k}} \). (6.1)

However, now that the centres have moved, the indicator vectors \( \mathbf{z}_n \) have to be adjusted. This can be viewed as minimizing \( J \) with respect to all \( \mathbf{z}_n \). This in turn will cause the centres to move again. The algorithm alternates between moving the centres \( \boldsymbol{\mu}_k \) and recalculating \( \mathbf{z}_n \). It terminates, when after moving the centres, none of the indicator vectors changes.

Looking at (6.1), note that \( \sum_{n=1}^N z_{n,k} \) gives the number of data samples for which \( \mu_k \) is the closest centre, while \( \sum_{n=1}^N z_{n,k} \mathbf{v}_n \) is the sum of those samples. Thus \( \mu_k \) is the mean of the samples assigned to this particular cluster.

The algorithm arrives at a local minimum of \( J \). However, this is by no means necessarily a global minimum. In fact, the solution is highly dependent on the initialization of the cluster centres. These can be chosen randomly at the start, or the samples can be randomly assigned clusters and the initial cluster centres be calculated as the mean of these random assignments. To counter this dependency on initial values, the algorithm is run (possibly in parallel) with many different initializations. After convergence, the result with the lowest value of \( J \) is chosen.

The squared Euclidean norm of the difference between sample and cluster centre was used. The algorithm can be generalized using any dissimilarity measure between two feature vectors, just as kernels were used as similarity measures for the kernel trick described in Section 5.2. In this case, the method is known as \( K \)-medoids algorithm. However, the minimization with regards to \( \mu_k \) might be much more involved. It depends on the differentiability of the dissimilarity measure, and whether it is possible to find where the derivative vanishes. If this is not possible, it is common practice to require each cluster centre to be one of the data samples. The minimization with respect to \( \mu_k \) is then a search among the data samples assigned to the \( k^{\text{th}} \) cluster.

Lossy data compression is achieved by choosing a suitable number of clusters and storing the feature vectors of the centres, \( \mu_k \). For each data sample only the cluster it belongs to is stored. This can be applied to images. Typically images are represented by storing three values for each pixel, with each ![](img/d3c00252180686426c9e63ab889b535b_172_0.png)

![](img/d3c00252180686426c9e63ab889b535b_172_1.png)

(a) K = 4, 8.3% compression ratio.

(b) K = 16, 16.7% compression ratio.

Figure 6.2: K mean compression.

value being one byte. Since one byte is 8 bits, 24N bits are necessary to store an image with N pixels. If instead we cluster the pixels using K clusters, we need to store the pixel values of each cluster centre which requires 24K bits. The cluster number can be encoded in $\log_2 K$ bits, and this needs to be stored for each pixel. For example, for K = 4, two bits are necessary. The cluster numbers are stored as 00,01,10,11. When K = 16, four bits are required. Figure 6.2 illustrates this. Using 4 clusters results in an image consisting of lighter and darker shades of brown which means the cluster centres did not stray too far off the axis of shades of gray where the red, green and blue components are equal. 16 clusters seem an adequate representation at a compression ratio of 16.7%. The colours are more realistic.

Listing 6.1 reads an image of tissue stained with hematoxylin and eosin to make different tissue types distinguishable (Image courtesy of Alan Partin, Johns Hopkins University). Using three clusters, one of these identifies the nuclei.

We used K means clustering on two examples of image processing. This is a very large area of ongoing research with algorithms tailored to specific applications. A comprehensive overview can be found in [18].

### 6.2 Mixture Models

Let's change our view point and say that the indicator variable $\mathbf{z}_n$ does not indicate to which cluster the sample $\mathbf{v}_n$ belongs, but shows which process generated that data sample, and we assume there are K distinct processes generating the data. Let $p_k(v)$ be the probability distribution of the samples generated by the kth process. Let $\pi_k$ be the probability that process k
