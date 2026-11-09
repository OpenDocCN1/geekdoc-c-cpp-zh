apace, some, now so convoluted and specific to a data type and application, that many fall outside the domain of this book [46, 61, 72, 143].

New clustering algorithms continue to appear in the literature across many domains, often merely modifications of already well known algorithms to suit a specific application. One can design new clustering algorithms, but it is often prudent to thoroughly review the literature, and not just within the broad application domain—there is a strong likelihood that a new algorithm or one nearly identical to it has already been published.

Cluster analysis as an exploratory data analysis tool is dependent on the ability to visually display results and thereby help interpret the results. Thus, the visualization of clustering results has received a boost in recent years with advances in high end computer graphics, but there is still a great deal of work to be done to effectively visualize the clustering results of large data sets or data sets with large dimensions. Multivariate analysis contributes important methods aligned with cluster analysis such as principal component analysis (PCA) [80] and various forms of multi-dimensional scaling (MDS) techniques, useful for both exploratory data analysis, and data and cluster visualization [16, 31]. PCA has also been used to develop clustering algorithms for gene expression data [154]. More recently, similar methods such as non-negative matrix factorization [34] have been developed and used for both exploratory analysis and modified for cluster analysis. These tools have their drawbacks as well however, and often a combination of visualization techniques are used to help visualize the results. Hierarchies in the form of *dendrograms* can now be represented in a number of different ways and are often shown in conjunction with *heatmaps*, helping to reveal the structure relationships in the data.

Cluster analysis in bioinformatics has three common applications: gene expression data, sequence analysis, and phylogenetic tree construction. The development of gene expression screening processes led to the development of cluster analysis for the interpretation of those data. Two process forms were developed in the 1990s that test the expression of thousands of genes at once on microarrays, either cDNA or oligonucleotide arrays. Regardless of the form of the arrays used, or of the types of experiments, the general form of the data are a matrix, where the rows represent the genes and the columns represent the experiments. In some instances the experiments represented time series data.

**Experiments**

**Genes**

( x_{1,1}  x_{1,2}  ...  x_{1,m}
  x_{2,1}  x_{2,2}  ...  x_{2,m}
  ...       ...      ...  ...
  x_{n,1}  x_{n,2}  ...  x_{n,m} )

Expression data are typically in the thousands, and the experiments are in the tens, and rarely more than one hundred. Thus, in the matrix above, n ≫ m. Larger expression data sets are now possible in the tens of thousands and may soon be in the hundreds of thousands to near one million. The first