further inspection. The conformation of the expected results is still speculative in some sense, but it provides some reassurance that the researchers methods are performing as expected.

# 10.4  Glossary

**clustering tendency:** whether or not a data set has internal structure at a specified scale

**external clustering validity:** comparing clusters to known classifications

**internal clustering validity:** determining the homogeneity and the separation of a clustering

**Monte Carlo integration:** approximating an integral with random sampling

**random graphs:** graphs that are generated under different probability models

# 10.5  Exercises

+   1. Implement Kelley's level selection [83] and apply it to small data sets clustered hierarchically [133] with several hierarchical algorithms. Compare and discuss results.
+   
+   2. Outline Monte Carlo integration and in what context might it be applied to cluster validation. Search the literature for recent applications of Monte Carlo to cluster validation and discuss the merits of using Monte Carlo versus other validation techniques.
+   
+   3. Hartigan suggested the following rule of thumb [63] for determining the appropriate $K$ in $K$-means:

$K+1$ groups is a better clustering than $K$ groups if

$$\Delta = \frac{\sum_{i=1}^{K} S_i^K}{\left(\sum_{i=1}^{K+1} S_i^{K+1}\right)/(N-K-1)} > 10 \qquad (10.10)$$

where $N$ is the total number of data items, and $S_i^K$ and $S_i^{K+1}$ are the