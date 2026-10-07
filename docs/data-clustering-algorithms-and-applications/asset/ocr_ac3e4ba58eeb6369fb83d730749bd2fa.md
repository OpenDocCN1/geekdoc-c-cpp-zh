# Clustering High-Dimensional Data

CLTree [96] is a method that presents an interesting variation of the theme. The basic idea is to assign a common class label to all existing points and additionally points uniformly distributed over the data space, clustering them. Then a decision-tree is trained to separate the two classes. As a consequence, attributes split independently, adaptively, and in a flexible order of attributes. However, selecting a split is based on the evaluation of information gain which is rather costly. Furthermore, the density of the superimposed artificial data can be expected to heavily influence the quality of the results. The distribution of existing clusters are unknown beforehand, finding a suitable parameterization seems rather hard. Another problem is the merging of adjacent regions. A cluster can easily be separated if the separating bins do not "touch" each other.

**Soft Clustering.** There is a rich literature concerned with so-called soft clustering [43, 55, 79, 28, 42, 98]. These are useful optimization approaches derived from k-means clustering, using some weight vector for the weighting of attributes. Thereof, weights $w_i$ for $i=1, \dots, d$ are introduced over the distance measure:

```
$$$\|(x-y)\|_p^p = \sum_{i=1}^{d} w_i |x_i - y_i|^p$$
```

Usually, in these approaches, weights are restricted to at least the condition

```
$0 < w_i \leq 1,$$
```

i.e., to ensure the applicability of optimization techniques, no attribute is truly omitted, and hence the resulting clustering resides in the full-dimensional, though skewed data space. The fact that the clustering is not truly searched for in a projected space (i.e., no subspace is assigned to a specific cluster) is indicated by the term soft. However, these approaches are generally named "subclustering," which reflects the differences discussed here. Essentially, all these approaches can be seen as variants of EM-clustering [40].

Geometrically, the effect of these approaches is just to allow the shape of clusters to become axis-parallel ellipsoids of spheres. This does not necessarily account for relevance or irrelevance of different attributes. It relates more to some sort of normalization of attributes per clusters.

An example for these methods is LAC (Locally Adaptive Clustering) [43], which starts with $k$ centroids and $k$ sets of $d$ weights (for d attributes). The algorithm proceeds to approximate a set of $k$ Gaussians by adapting the weights.

COSA [55], another prominent example, does not define a clustering but merely a similarity matrix that can be used by an arbitrary clustering algorithm. The matrix contains weights for each point a subspace preference of the points to PreDeCon. The weights for a point $p$ are determined by starting with the Euclidean $k$-nearest neighbors of $p$ and by computing the average distance distribution along each dimension. Roughly, the weight for a given attribute is the ratio between the distances of the point $p$ to all $k$-nearest neighbors of $p$ in all attributes. The higher the variance of the $k$-nearest neighbors along an attribute is, the higher the weight that is assigned to that attribute. The weight, however, cannot become 0. As long the vector weights still change, the $k$-nearest neighbors are again determined using the current weights and the number of neighbors is an input parameter. Very different from PreDeCon, the weights can have arbitrary values rather than two fixed values. In addition, the weighting matrix is tested using several full-dimensional clustering algorithms rather than integrating it into only one specific algorithm. Note that the effect of weight vectors is very different in density-based approaches like PreDeCon where the shape of clusters is not defined beforehand.