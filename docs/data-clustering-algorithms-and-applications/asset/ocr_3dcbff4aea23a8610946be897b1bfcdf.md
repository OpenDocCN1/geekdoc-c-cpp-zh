# Data Clustering: Algorithms and Applications

where N is the total number of samples (columns or features). $g_k$ represents the kth column of vector $g_i$. One of the problems with Euclidean distance measure is its inability to capture shifting and scaling patterns that commonly occur in expression data [2]. To solve this, these gene vector are Z-score normalized by subtracting the mean of the gene vector from individual column values and dividing them by the variance of the original gene vector [20]. This will make the mean of the resultant vector zero and the variance one for each gene vector.

+   * Spearman correlation coefficient: To make the similarity measure robust to the underlying distributions and outliers, Spearman correlation considers the rank ordering of the expression values. Rather than using the original expression values for each gene, the Spearman correlation coefficient uses the rank of each sample value for that particular gene [56]. It is defined to be the Pearson correlation coefficient between the ranked expression values. Since the original expression values are discarded, the results from this measure are almost always inferior to those using Pearson correlation coefficient in the context of standard gene clustering.

+   * Mutual Information: Mutual Information (MI) is an information-theoretic approach which uses a generalization of pairwise correlation coefficient to compare two gene expression files. MI can be used to measure the degree of independence between two genes [19]. The MI between a pair of genes $g_i$ and $g_j$ is computed as follows:
$$MI_{ij} = H_i + H_j - H_{ij}$$

where H denotes the entropy is given as follows:
$$H_i = -\sum_{k=1}^{N} p(g_{ik})log(p(g_{ik}))$$

It can be seen that the higher the entropy, the more distributed are the gene expression levels across the conditions. Also, if the expression levels of genes i and j are statistically independent then their joint entropy $H_{ij}=H_i+H_j$. A higher value of MI indicates that the genes are nonrandomly associated to each other. Even though MI shown some promising results in the context of clustering [83], it is more widely used in the context of constructing gene co-expression networks.

# 16.2.2 Categorization of Algorithms

The existing methods can be categorized into the following groups as shown below. Each of these categories will be explained more elaborately in this section.