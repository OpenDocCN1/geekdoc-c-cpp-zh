plot displaying asymmetric drift for a set of ligands. The asymmetric drift is represented by the arrows. The green dots represent the MDS placement of the symmetric proximity matrix and the red circles represent a scaled variable property.

![](bbox=[0.118, 0.195, 0.942, 0.612])

FIGURE 2.10: Example asymmetric drift plot. The centers of the circles represent the symmetric placement in MDS, the arrows represent the asymmetric drift, the circles represent a scaled property.

# ### 2.8.2 Hadamard Product of Two Matrices

Hadamard product matrices have other uses in clustering aside from exploring asymmetric matrix properties. Symmetric matrices can be used to compose other symmetric matrices. For example, matrices A and B may be matrices generated different dissimilarity measures over the same data. In one such example, the molecular shape Tanimoto and the electrostatic Tanimoto matrices can be composed with the Hadamard product, and once suitably normalized, the result can be used as a proximity matrix for clustering. The composition of these two measures can be made via the Hadamard product, but properties of both matrices and the Hadamard product thereof may determine what possible further clustering algorithms or statistical analysis such as PCA or MDS can be performed. If, say, the two matrices are positive semi-definite. The Hadamard product of the two matrices is not necessarily so.