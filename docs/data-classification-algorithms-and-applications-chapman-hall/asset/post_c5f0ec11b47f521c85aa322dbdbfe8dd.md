
by a bag of words with c(vi,xj) to denote the frequency of word vi in xj. Without loss of generality, we use a unified vocabulary W for all domains, and assume |W| = m.

For each sentiment data xj, there is a corresponding label yj, where yj = +1 if the overall sentiment expressed in xj is positive, and yj = -1 if the overall sentiment expressed in xj is negative. A pair of sentiment text and its corresponding sentiment polarity {xj,yj} is called the labeled sentiment data. If xj has no polarity assigned, it is unlabeled sentiment data. Note that besides positive and negative sentiment, there are also neutral and mixed sentiment data in practical applications. Mixed polarity means user sentiment is positive in some aspects but negative in other ones. Neutral polarity means that there is no sentiment expressed by users. In this chapter, we only focus on positive and negative sentiment data.

For simplicity, we assume that a sentiment classifier f is a linear function as

$$y^* = f(x) = \text{sgn}(w^T x),$$

where x ∈ ℝ^{m×1}, sgn(w^T x) = +1 if w^T x ≥ 0, otherwise, sgn(w^T x) = -1, and w is the weight vector of the classifier, which can be learned from a set of training data (i.e., pairs of sentiment data and their corresponding polarity labels).

Consider the example shown in Table 21.1 as a motivating example. We use the standard bag-of-words representation to represent sentiment data of the Electronics and Video Games domains. From Table 21.2, we observe that the difference between domains is caused by the frequency of the domain-specific words. On one hand, the domain-specific words in the Electronics domain, such as compact, sharp and blurry, cannot be observed in the Video Games domain. On the other hand, the domain-specific words in the Video Games domain, such as hooked, realistic and boring, cannot be observed in the Electronics domain. Suppose that the Electronics domain is the source domain and the Video Games domain is the target domain. Apparently, based on the three training sentences in the Electronics domain, the weights of the features compact and sharp are positive, the weight of the feature blurry are negative, and the weights of the features hooked, realistic and boring can be arbitrary or zeros if an ℓ1-norm regularization term is performed on w for model training. However, an ideal weight vector for the Video Games domain are supposed to have positive weights on the features hooked, realistic and a negative weight on the feature boring. Therefore, a classifier learned from the Electronics domain may predict poorly or randomly on the Video Games domain data.

**TABLE 21.2**: Bag-of-Words Representations of Electronics and Video Games Reviews.

|   |   | compact | sharp | blurry | hooked | realistic | boring |
|---|---|---|---|---|---|---|---|
| electronics | +1 | 1 | 1 | 0 | 0 | 0 | 0 |
| electronics | +1 | 0 | 1 | 0 | 0 | 0 | 0 |
| electronics | -1 | 0 | 0 | 1 | 0 | 0 | 0 |
| video games | +1 | 0 | 0 | 0 | 1 | 0 | 0 |
| video games | +1 | 0 | 0 | 0 | 1 | 1 | 0 |
| video games | -1 | 0 | 0 | 0 | 0 | 0 | 1 |

Note: Only domain-specific features are considered.

Generally speaking, in sentiment classification, features can be classified into three types:

- 1) source domain (i.e., the Electronics domain) specific features, such as compact, sharp, and blurry,
- 2) target domain (i.e., the Video Game domain) specific features, such as hooked, realistic, and boring, and
- 3) domain independent features or pivot features, such as good, excited, nice, and never_buy.

Based on these observations, an intuitive idea of feature learning is to align the source and target domain specific features to generate cluster- or group- based features by using the domain independent features as a bridge such that the difference between the source and target domain data based on the new feature representation can be reduced. For instance, if the domain specific features shown in Table 21.2 can be aligned in the way presented in Table 21.3, where the feature alignments are used as new features to represent the data, then apparently, a linear model learned from the source domain (i.e., the Electronics domain) can be used to make precise predictions on the target domain data (i.e., the Video Game domain).

**TABLE 21.3**: Using Feature Alignments as New Features to Represent Cross-Domain Data.

|   |   | sharp_hooked | compact_realistic | blurry_boring |
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

Pan et al. [92] proposed the Spectral Feature Alignment (SFA) method for aligning domain specific features, which shares a similar high-level motivation with SCL. Instead of constructing pseudo tasks to use model parameters to capture the correlations between domain-specific and domain-independent features, SFA aims to model the feature correlations using a bipartite graph. Specifically, in the bipartite graph, a set of nodes correspond to the domain independent features, and the other set of nodes correspond to domain specific features in either the source or target domain. There exists an edge connecting a domain specific feature and a domain independent feature, if they co-occur in the same document or within a predefined window. A number associated on an edge is the total number of the co-occurrence of the corresponding domain specific and domain independent features in the source and target domains. The motivation of using a bipartite graph to model the feature correlations is that if two domain specific features have connections to more common domain independent features in the graph, they tend to be aligned or clustered together with a higher probability. Meanwhile, if two domain independent features have connections to more common domain specific features in the graph, they tend to be aligned together with a higher probability. After the bipartite graph is constructed, the spectral clustering algorithm [88] is applied on the graph to cluster domain specific features. In this way, the clusters can be treated as new features to represent cross-domain data.

### 21.3.2.2 Learning Features by Minimizing Distance between Distributions

In the previous section, we have shown how to encode domain knowledge into feature learning for transfer learning. However, in many real-world scenarios, domain knowledge is not available as input. In this case, general approaches to feature learning for transfer learning are required. In this section, we first introduce a feature learning approach to transfer learning based on distribution minimization in a latent space.

Note that in many real-world applications, the observed data are controlled by only a few latent factors. If the two domains are related to each other, they may share some latent factors (or components). Some of these common latent factors may cause the data distributions between domains to be different, while others may not. Meanwhile, some of these factors may capture the intrinsic structure or discriminative information underlying the original data, while others may not. If one can recover those common latent factors that do not cause much difference between data distributions and do preserve the properties of the original data, then one can treat the subspace spanned by these latent factors as a bridge to make knowledge transfer possible. Based on this motivation, Pan et al. [90] proposed a dimensionality reduction algorithm for transfer learning, whose high-level idea can be formulated as follows:

$$\begin{aligned}
\min_{\varphi}\quad & \operatorname{Dist}(\varphi(X_S),\varphi(X_T)) + \lambda\Omega(\varphi) \\
\text{s.t.}\quad & \text{constraints on }\varphi(X_S)\text{ and }\varphi(X_T),
\end{aligned}\tag{21.7}$$

where φ is the mapping to be learned, which maps the original data to a low-dimensional space. The first term in the objective of (21.7) aims to minimize the distance in distributions between the source and target domain data, Ω(φ) is a regularization term on the mapping φ, and the constraints are to ensure original data properties are preserved.

Note that, in general, the optimization problem (21.7) is computationally intractable. To make it computationally solvable, Pan et al. [90] proposed to transform the optimization problem (21.7) to a kernel matrix learning problem, resulting in solving a semidefinite program (SDP). The proposed method is known as Maximum Mean Discrepancy Embedding (MMDE), which is based on the non-parametric measure MMD as introduced in Section 21.3.1.1. MMDE has proven to be effective in learning features for transfer learning. However, it has two major limitations:

- 1) Since it requires to solve a SDP, its computational cost is very expensive;
- 2) Since it formulates the kernel matrix learning problem in a transductive learning setting, it cannot generalize to out-of-sample instances.

To address the limitations of MMDE, Pan et al. [95, 96] further relaxed the feature learning problem of MMDE to a generalized eigen-decomposition problem, which is very efficient and easily generalized to out-of-sample instances. Similarly, motivated by the idea of MMDE, Si et al. [125] proposed to use the Bregman divergence as the distance measure between sample distributions to minimize the distance between the source and target domain data in a latent space.
