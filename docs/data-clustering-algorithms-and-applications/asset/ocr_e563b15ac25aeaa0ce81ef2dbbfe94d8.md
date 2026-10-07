# Feature Selection for Clustering: A Review

where $p(f,c)$ is the probability of class $c$ that contains term $f$, and $p(
eg f,
eg c)$ is the probability of not being in $c$ and not containing term $f$ and so on. $\chi^2$ cannot be directly applied in an unsupervised learning clustering due to the absence of class label. Li et al in [34] propose a variation of $\chi^2$ that overcomes drawbacks of the original $\chi^2$ and is embedded in an Expectation-Maximization (EM) algorithm to be used for clustering problems. [34] found out that $\chi^2$ cannot determine whether the dependency between the feature and the class is negative or positive, which leads to ignoring relevant features and selecting irrelevant features. Therefore, they propose a relevance measure ($R$) that can be used in the original $\chi^2$ to overcome this limitation. This new measure $R$ follows

```
$R(f,c) = \frac{p(f,c)p(\neg f,\neg c)}{p(\neg f,c)p(f,\neg c)} \quad\quad\(2.12)$
```

$R$ in Equation (2.12) will be equal to 1 if there is no such dependency between the class and the feature, greater than 2 if there is a positive dependency, and less than 1 if the dependency is negative.
From Equations (2.11) and (2.12), Hoffman et al. [34] propose a new variation of $\chi^2$ that is able to distinguish positive and negative relevance:

```
$$\chi^2(f) = \sum_{j=1}^{k} p(f,c_j)^2 p(c_j) \quad\quad\(2.13)$
```

where $p(R,c)$ is given by $p(R(f,c)) = \frac{R(f,c)}{\sum R(f,c)}$. The larger the value of $\chi^2$ is, the more relevant the feature $f$ will be.
As we mentioned earlier, we cannot apply a supervised feature selection in an unsupervised learning directly. Therefore, [34] embedded their proposed method in Equation (2.13) in a clustering algorithm using EM approach. They used $k$-means as the clustering algorithm and $\chi^2$ as the feature selection method as shown in Algorithm 5.

Algorithm 5 $\chi^2$ as a feature selector for clustering

+   **Input:**
D: dataset
k: number of clusters
$\alpha$: predetermine parameter in the range of [0,1]
m: number of selected features
**Output:**
C the clusters
**Initialize:**
$C \leftarrow k$-means on $D$ to obtain initial clusters

+   1. **E-step:**
- Apply $\chi^2$ from Equation (2.13) using clusters $C$ obtained from step (1) as class labels.
- Make the weight of the top $m$ relevant features 1 and $\alpha$ for the rest of the features.
- Calculate the new $k$-centroid for the new space.

+   2. **M-step:** Compute the clusters using $k$-means.

+   3. **Repeat** E-step and M-step until convergence.