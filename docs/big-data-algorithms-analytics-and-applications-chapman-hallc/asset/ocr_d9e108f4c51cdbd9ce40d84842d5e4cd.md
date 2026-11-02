# 3.2 DATA REDUCTION METHODS AND SVD

Data reduction methods are of interest in several domains, such as query cost estimation in relational databases [19], data mining, decision support, online analytical processing (OLAP) [20], data compression, information retrieval, and data visualization. We list the data reduction methods surveyed in Reference 21 as follows:

+   1. SVD, PCA, and KLT are related dimensionality reduction methods, which are discussed in this section.
+   2. Discrete wavelet transform (DWT) has many variations [13], such as Daubechies transform [22]. It has been utilized in Reference 23 for data compression in a relational database.
+   3. Regression, in its simplest form, is the linear regression of a single variable model, that is, variable Y as a linear function of variable X, Y = α + βX, but regression can be extended to more than one variable [13].
+   4. Log-linear models are a methodology for approximating discrete multidimensional probability distributions; for example, the multiway table of joint probabilities is approximated by a product of lower-order tables [24].
+   5. Histograms approximate the data in one or more attributes of a relation by their frequencies [25].
+   6. Clustering techniques are discussed in Section 3.3.
+   7. Indexing structures are discussed in Section 3.7.
+   8. Sampling is an attempt to represent a large set of data by a small random sample of its data elements. Sampling in databases is reviewed in Reference 26, and Reference 27 is a representative publication.

We only consider SVD and related methods in our discussion in the context of the discussion in References 3 and 14. Consider matrix X, whose M rows are the feature vectors for images. Each image has N features, which is the number of columns in the matrix. Subtracting the mean from the elements in each column yields columns with a zero mean. The columns may be furthermore studentized by dividing the elements by the standard deviation. The SVD of X is given as follows [8,28]:

X = U Σ V^T, (3.1)

where U is an M × N column-orthonormal matrix, V is an N × N unitary matrix of eigenvectors, and Σ is a diagonal matrix of singular values, without loss of generality (σ₁ ≥ σ₂ ≥ …, ≥ σ_N). When the number of singular values that are not zero or close to zero is n, then the rank of X is n [8]. The cost of computing eigenvalues using SVD is O(MN)². The following example shows the decomposition of X and that it has a rank of three, since two of its eigenvalues are zero.