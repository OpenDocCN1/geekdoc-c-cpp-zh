used as new features to represent the data, then apparently, a linear model learned from the source domain (i.e., the Electronics domain) can be used to make precise predictions on the target domain data (i.e., the Video Game domain).

# TABLE 21.3: Using Feature Alignments as New Features to Represent Cross-Domain Data.

| | | sharp_hooked | compact_realistic | blurry_boring |
|---|---|---|---|---|
| electronics | +1 | 1 | 1 | 0 |
| electronics | +1 | 1 | 0 | 0 |
| electronics | -1 | 0 | 0 | 1 |
| video games | +1 | 1 | 0 | 0 |
| video games | +1 | 1 | 1 | 0 |
| video games | -1 | 0 | 0 | 1 |

Therefore, there are two research issues to be addressed. A first issue is how to identify domain independent or pivot features. A second issue is how to utilize the domain independent features and domain knowledge to align domain specific features from the source and target domains to generate new features. Here the domain knowledge is that if two sentiment words co-occur frequently in one sentence or document, then their sentiment polarities tend to be the same with a high probability.

For identifying domain independent or pivot features, some researchers have proposed several heuristic approaches [18,92]. For instance, Blitzer et al. [18] proposed to select pivot features based on the term frequency in both the source and target domains and the mutual dependence between the features and labels in the source domain. The idea is that a pivot feature should be discriminative to the source domain data and appear frequently in both the source and target domains. Pan et al. [92] proposed to select domain independent features based on the mutual dependence between features and domains. Specifically, by considering all instances in the source domain with labels 1’s and all instances in the target domain with labels 0’s, the mutual information can be used to measure the dependence between the features and the constructed domain labels. The motivation is that if a feature has high mutual dependence to the domains, then it is domain specific. Otherwise, it is domain independent.

For aligning domain specific features from the source and target domains to generate cross-domain features, Blitzer et al. [19] proposed the structural correspondence learning (SCL) method. SCL is motivated by a multi-task learning algorithm, alternating structure optimization (ASO) [4], which aims to learn common features underlying multiple tasks. Specifically, SCL first identifies a set of pivot features of size m, and then treats each pivot feature as a new output vector to construct a pseudo task with non-pivot features as inputs. After that, SCL learns m linear classifiers to model the relationships between the non-pivot features and the constructed output vectors as follows,

y_j = sgn(w_j^T x_np), j = 1, ..., m,

where y_j is an output vector constructed from a corresponding pivot feature, and x_np is a vector of non-pivot features. Finally, SCL performs the singular value decomposition (SVD) on the weight matrix W = [w1 w2 ... wm] ∈ R^{q×m}, where q is the number of non-pivot features, such that W = U D V^T, where U_{q×r} and V_{r×m} are the matrices of the left and right singular vectors. The matrix D_{r×r} is a diagonal matrix consisting of non-negative singular values, which are ranked in non-increasing order. The matrix U^T_{[1:h,:]}, where h is the number of features to be learned, is then used as a transformation to align domain-specific features to generate new features.

Pan et al. [92] proposed the Spectral Feature Alignment (SFA) method for aligning domain specific features, which shares a similar high-level motivation with SCL. Instead of constructing pseudo tasks to use model parameters to capture the correlations between domain-specific and domain-independent features, SFA aims to model the feature correlations using a bipartite graph. Specifically, in the bipartite graph, a set of nodes correspond to the domain independent features,