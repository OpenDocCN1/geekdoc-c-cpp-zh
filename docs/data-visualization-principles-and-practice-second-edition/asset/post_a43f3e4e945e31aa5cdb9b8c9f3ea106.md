
and detecting one is surprisingly difficult in practice. Many methods for vortex detection have been designed over the last 15 years [Banks and Singer 95, Jankun-Kelly et al. 06]. For an overview of this topic, we point the reader to existing review papers [Post et al. 02, Post et al. 03b].

Although feature detection methods can give good results, they do not come without problems. First, it is hard to define precise numerical criteria to detect such features. For example, it is difficult to precisely quantify the presence and/or extent of a vortex. Second, features appear at different spatial scales in vector fields. In time-dependent fields, there exist also different temporal scales. Finally, there is often no clear spatial separation between a feature and a non-feature area or between several features of the same or different types.

### 6.7.3 Field Decomposition Methods

The third class of methods is formed by field decomposition methods. Such methods partition the vector dataset into regions of strong intraregion (inter-region) similarity and weak interregion similarity. At the core of such methods is a similarity metric f that defines how similar two regions are. Different similarity metrics lead to different decompositions that model different end goals or questions. A frequently used similarity metric compares the direction and magnitude of the vector data. Two regions are considered highly similar if the vector field has the same orientation and magnitude on both regions, and dissimilar otherwise. After choosing the metric, decomposition methods usually perform a top-down partitioning or bottom-up agglomerative clustering of the dataset. In the top-down case, the dataset is recursively split in regions that have the least similarity. In the bottom-up case, we start with each sample point (or equivalent small area) being a different region and iteratively cluster the most similar regions. Both methods produce a multiscale representation of the vector dataset that can be seen as a tree with the smallest regions, or data samples, as leaves and the whole dataset as the root. A desirable constraint for decomposition methods is to produce spatially compact regions, since these are easier to visualize and interpret, and also map well to the “natural” idea of what a vector field feature is. For top-down methods, this constraint can be added in the splitting step. For bottom-up methods, the constraint can be added either in the similarity metric (non-neighboring regions have minimal similarity) or the merging logic (non-neighboring regions are never merged).

### Top-down decomposition

An example of a top-down decomposition method is the technique by Heckel et al. [Heckel et al. 99]. Initially, all data points bearing vectors are placed in a single cluster. Next, this cluster is repeatedly subdivided using a weighted best-fit plane so that the variance of an error metric over its two children is minimized. For each cluster, a representative vector is computed as the average of the vector samples in that cluster. The error of a given split is defined as the difference between streamlines traced in the original field and the simplified one given by the representative vectors. This method produces a vector field simplification that directly encodes elements of the visualization itself: a “good” simplification is that which produces streamlines close to the original field.

### Bottom-up decomposition

Many bottom-up clustering methods exist, and many are based on work on discrete and continuous data clustering performed outside of the visualization domain [Jain and Murty 99]. A simple bottom-up strategy is to use a greedy approach. We define a region as the triplet \(R = (P(R), \mathbf{v}(R), O(R))\). Here, \(P(R) = \{p_i\}\) is the set of sample points, or support, of the region, which is compact from the perspective of the point neighbor relationship. The simplest way we can represent the vector field over \(P(R)\) is by a single vector \(\mathbf{v}(R)\) located at an origin \(O(R)\) inside the area covered by \(P(R)\). We begin the clustering by defining, for every point \(p_j\) of the dataset, a region \(R_j = (p_j, \mathbf{v}(p_j), p_j)\) containing the point and its vector attribute that has the origin at the point itself. The complete region set \(\mathcal{R} = \{R_i\}\) is next simplified iteratively by clustering, at every step, the two most-similar regions \(R_a \in \mathcal{R}, R_b \in \mathcal{R}\) to form a new region \(R_{ab}\). This new region contains the union of all points in \(R_a\) and \(R_b\) and a vector \(\mathbf{v}(R_{ab})\) that should best reflect the merging of \(R_a\) and \(R_b\). A simple way to compute \(\mathbf{v}(R_{ab})\) is as the average of \(\mathbf{v}(R_a)\) and \(\mathbf{v}(R_b)\) weighted by the number of points \(|P(a)|\) and \(|P(b)|\) in the merged regions. The origin \(O(R_{ab})\) of \(\mathbf{v}(R_{ab})\) can be computed similarly to the computation of \(\mathbf{v}(R_{ab})\) by weighted averaging. This technique is also known as bottom-up agglomerative clustering with average linkage, since a cluster is represented by, and compared with other clusters with, a single average vector. Finally, we set \(R_a\) and \(R_b\) as children of \(R_{ab}\), so that a binary region tree, or dendrogram, gets constructed during the clustering. The complete algorithm is described in Listing 6.3.

From the initial \(\mathcal{R}^1\), the clustering creates region sets \(\mathcal{R}^1, \dots, \mathcal{R}^F\) until reaching a final region set \(\mathcal{R}^F\) that contains a user-specified number of \(N\) regions.

6 A generic, easy to use, and efficient C implementation of bottom-up hierarchical agglomerative clustering, offering different linkage strategies and user-specified distance metrics, is provided by the Cluster library, publicly available at http://bonsai.hgc.jp/~mdehoon/software/ cluster.

### Listing 6.3. Bottom-up greedy clustering of vector data.

```
initialize the starting region set R^0;
for (int i=0;|R^i|>N;i++)
{
    find R_a in R^i, R_b in R^i so that f(R_a,R_b) = min;
    v(R_ab) = (v(R_a)|P(R_a)| + v(R_b)|P(R_b)|)/(|P(R_a)| + |P(R_b)|);
    O(R_ab) = (O(R_a)|P(R_a)| + O(R_b)|P(R_b)|)/(|P(R_a)| + |P(R_b)|);
    R_ab = (P(R_a) U P(R_b), v(R_ab), O(R_ab));
    R^{i+1} = R^i - {R_a U R_b}; //eliminate R_a and R_b from R^{i+1}
    R^{i+1} = R^{i+1} U {R_ab}; //add the new R_ab to R^{i+1}
    set R_a and R_b as children of R_ab;
}
```

These regions are the roots of several region trees that encode the clustering, as described previously. We can use these trees to obtain several types of simplified representations of our vector field. A simplified representation, or s-rep, is a region set R = {R_1, ..., R_k} of k disjoint regions where each R_i is a node in a different region tree described earlier and whose union \(\cup_{l=1}^k R_l\) covers the complete dataset.

Having such a s-rep, a visualization of the vector field can be produced by displaying the representative vectors for all regions, streamlines seeded at the region origins and clipped by the region boundaries, or the regions themselves colored in different colors (the last option is effective mainly for 2D domains). By controlling N, one can answer the question “show a vector field with N curved arrows.” Figure 6.32 shows such visualizations for 2D and 3D vector fields. The similarity metric used favors vectors with the same direction and magnitude, which explains the elongated shapes of the regions shown in Figure 6.32(a). In Figure 6.32(b), arrow-capped stream tubes are drawn for every region and an additional horizontal slice plane, tubed with a spot noise visualization of the vector field, is used to provide an extra visual cue.

Several s-reps can be created from the region trees. The easiest is to use any of the region sets R^i constructed during the clustering. However, choosing which level i to look at is not very intuitive, as we do not know how many regions R^i has. Other options for constructing the s-rep are to take regions at a user-given depth from the root in the region trees or an s-rep containing a user-specified number of N regions. Since the decomposition is saved in the region trees, dynamically
