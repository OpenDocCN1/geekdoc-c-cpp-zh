
# FIGURE 15.1 (See color insert.): (a) An illustration of the common i.i.d. supervised learning setting. Here each instance is represented by a subgraph consisting of a label node (blue) and several local feature nodes (purple). (b) The same problem, cast in the relational setting, with links connecting instances in the training and testing sets, respectively. The instances are no longer independent. (c) A relational learning problem in which each node has a varying number of local features and relationships, implying that the nodes are neither independent nor identically distributed. (d) The same problem, with relationships (links) between the training and test set.

node i, let N_i denote the set of indices corresponding to its (open) neighborhood; that is, the set of nodes adjacent to i (but not including it).

## 15.2.1 Inductive vs. Transductive Learning

Learning scenarios for collective classification broadly fall into two main categories: inductive and transductive. In inductive learning, data is assumed to be drawn from a distribution over the domain; that is, a sentence, image, social network, or some other data structure is generated according to a distribution over instances of said structure. Given a number of labeled structures drawn from this distribution, the objective is to learn to predict on new draws. In the transductive setting, the problem domain is fixed, meaning the data simply exists. The distribution from which the data was drawn is therefore irrelevant, since there is no randomness over what values could occur. Instead, randomness comes from which nodes are labeled, which happens via some stochastic sampling process. Given a labeled subset of the data, the goal is to learn to correctly predict the remaining instances.

In the inductive setting, one commonly assumes that draws of test examples are independent of the training examples. However, this may not hold with relational data, since the data-generating process may inject some dependence between draws from the distribution. There may be dependencies between nodes in the train and test data, as illustrated in Figure 15.1. The same is true of the transductive setting, since the training data may just be a labeled portion of one large network. The dependencies between training and testing must be considered when computing certain metrics, such as train and test accuracy [21].

Since collective methods leverage the correlations between adjacent nodes, researchers typically assume that a small subset of labels are given during prediction. In the transductive setting, these

nodes are simply the training set; in the inductive setting, this assumes that draws from the distribution over network structures are partially labeled. However, inductive collective classification is still possible even if no labels are given.

## 15.2.2 Active Collective Classification

An interesting subproblem in collective classification is how one acquires labels for training (or prediction). In supervised and semi-supervised learning, it is commonly assumed that annotations are given a priori—either adversarially, as in the online model, or agnostically, as in the probably approximately correct (PAC) model. In these settings, the learner has no control over which data points are labeled.

This motivates the study of active learning. In active learning, the learner is given access to an oracle, which it can query for the labels of certain examples. In active collective classification, the learning algorithm is allowed to ask for the labels of certain nodes, so as to maximize its performance using the minimal number of labels. How it decides which labels to query for is an open problem that is generally NP-hard; nonetheless, researchers have proposed many heuristics that work well in practice [4, 21, 27]. These typically involve some trade-off between propagation of information from an acquired label and coverage of the network.

The label acquisition problem is also relevant during inference, since the predictor might have access to a label oracle at test time. This form of active inference has been very successful in collective classification [3, 35]. Queries can sometimes be very sophisticated: a query might return not only a node’s label, but also the labels of its neighbors; if the data graph is uncertain, a query might also return information about a node’s local relationships (e.g., friends, citations, influencers, etc.). This has been referred to as active surveying [30, 38].

Note that an optimal label acquisition strategy for active learning may not be optimal for active inference, so separate strategies may be beneficial. However, the relative performance improvements of active learning and inference are easily conflated, making it difficult to optimize the acquisition strategies. [21] proposes a relational active learning framework to combat this problem.

## 15.3 Iterative Methods

Collective classification can in some sense be seen as achieving agreement amongst a set of interdependent, local predictions. Viewed as such, some approaches have sought ways to iteratively combine and revise individual node predictions so as to reach an equilibrium. The collective inference algorithm is essentially just a wrapper (or meta-algorithm) for a local prediction subroutine. One of the benefits of this technique is that local predictions can be made efficiently, so the complexity of collective inference is effectively the number of iterations needed for convergence. Though neither convergence nor optimality is guaranteed, in practice, this approach typically converges quickly to a good solution, depending on the graph structure and problem complexity. The methods presented in this section are representative of this iterative approach.

### 15.3.1 Label Propagation

A natural assumption in network classification is that adjacent nodes are likely to have the same label, (i.e., contagion). If the graph is weighted, then the edge weights {w_{i,j}}_{(i,j)∈E} can be interpreted as the strength of the associativity. Weights can sometimes be derived from observed features X via a similarity function. For example, a radial basis function can be computed between

adjacent nodes (i, j) as

$$w_{i,j} \triangleq \exp\left(-\frac{\|X_i - X_j\|_2^2}{\sigma^2}\right), \tag{15.1}$$

where σ is a parameter that determines the width of the Gaussian.

Suppose the labels are binary, with 𝒴ᵢ ∈ {±1} for all i = 1,…,n. If node i is unlabeled, we could predict a score for Yᵢ = 1 (or Yᵢ = −1) as the weighted average of its neighbors’ labels, i.e.,

$$Y_i \leftarrow \left(\frac{1}{\sum_{j\in\mathcal{N}_i} w_{i,j}}\right) \sum_{j\in\mathcal{N}_i} w_{i,j} Y_j.$$

One could then clamp Yᵢ to {±1} using its sign, sgn(Yᵢ). While we probably will not know all of the labels of 𝒩ᵢ, if we already had predictions for them, we could use these, then iterate until the predictions converge. This is precisely the idea behind a method known as label propagation. Though the algorithm was originally proposed by [48] for general transductive learning, it can easily be applied to network data by constraining the similarities according to a graph. An example of this is the modified adsorption algorithm [39].

Algorithm 15.1 provides pseudocode for a simple implementation of label propagation. The algorithm assumes that all labels are k-valued, meaning |𝒴ᵢ| = k for all i = 1,…,n. It begins by constructing a n × k label matrix Y ∈ ℝⁿˣᵏ, where entry i, j corresponds to the probability that Yᵢ = j. The label matrix is initialized as

$$\mathbf{Y}_{i,j} = \begin{cases} 1 & \text{if } Y_i \in \mathbf{Y}^\ell \text{ and } Y_i = j, \\ 0 & \text{if } Y_i \in \mathbf{Y}^\ell \text{ and } Y_i \neq j, \\ 1/k & \text{if } Y_i \in \mathbf{Y}^u. \end{cases} \tag{15.2}$$

It also requires an n × n transition matrix T ∈ ℝⁿˣⁿ; semantically, this captures the probability that a label propagates from node i to node j, but it is effectively just the normalized edge weight, defined as

$$\mathbf{T}_{i,j} = \begin{cases} \frac{w_{i,j}}{\sum_{j'\in\mathcal{N}_i} w_{i,j'}} & \text{if } j \in \mathcal{N}_i, \\ 0 & \text{if } j \notin \mathcal{N}_i. \end{cases} \tag{15.3}$$

The algorithm iteratively multiplies Y by T, thereby propagating label probabilities via a weighted average. After the multiply step, the unknown rows of Y, corresponding to the unknown labels, must be normalized, and the known rows must be clamped to their known values. This continues until the values of Y have stabilized (i.e., converged to within some sufficiently small ε of change), or until a maximum number of iterations has been reached.

**Algorithm 15.1 Label propagation**
1: Initialize Y per Equation (15.2)
2: Initialize T per Equation (15.3)
3: repeat
4:   Y ← TY
5:   Normalize unknown rows of Y
6:   Clamp known rows of Y using known labels
7: until convergence or maximum iterations reached
8: Assign to Yᵢ the jᵗʰ label, where j is the highest value in row i of Y.

One interesting property of this formulation of label propagation is that it is guaranteed to converge to a unique solution. In fact, there is a closed-form solution, which we will describe in Section 15.4.
