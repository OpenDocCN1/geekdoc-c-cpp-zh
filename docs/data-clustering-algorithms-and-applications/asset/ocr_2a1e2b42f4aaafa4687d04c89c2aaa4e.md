![](bbox=[0.211, 0.076, 0.796, 0.273])

**FIGURE 7.1:** Left: ORL face image dataset, containing 100 images of 10 persons. Middle/Right:
Computed NMF factors $F=(f_1, \dots, f_{16})$ for 2 runs with random initialization.

function attempts to capture. When the data distribution is far from a spherical clustering, NMF
can have advantages. Another advantage of NMF is that NMF can do both hard and soft clustering
simultaneously.

Figure 7.3 gives an example. The 2-D dataset in the left consists of 38 data points and the
G$ values are in the right figure. As seen in the figure, $G$ values for $\{C, D, E\}$nindicate they are fractionally assigned to different clusters. As a result, NMF is able to perform soft
clustering.

The third advantage is that NMF is able to perform simultaneously clustering of the rows (fea-
tures) and the columns (data points) of an input data matrix. Consider the following NMF objective
with orthonormal constraints on the factor matrices.

> $J_{orth} = \|X - FG^T\|^2, \text{ s.t. } F \ge 0, G \ge 0, F^TF = I, G^TG = I.$

The orthonormal constraints and the nonnegative constraints in Equation (7.9) make the resulted $F
and $G$ approximate the $K$-means clustering results on both features and data points [35]. The fourth
advantage is that many other data mining and machine learning problems can be reformulated as
NMF problems.

![](bbox=[0.211, 0.698, 0.796, 0.871])

**FIGURE 7.2:** Left: Digits image dataset. Middle/Right: Computed NMF factors $F=(f_1, \dots, f_{16})$nfor 2 runs with random initialization.