# 13.2.7 Approximate Structure Learning

Recall from Section 13.2.4 that when the number of variables is not small, it is computationally unfeasible to find the maximizing DAGs by exhaustively considering all DAGs. Therefore, researchers have developed heuristic search algorithms. We discuss such algorithms next.

# 13.2.7.1 K2 Algorithm

We present an algorithm in which the search space is the set of all DAGs containing n nodes, where n is our number of random variables. In these algorithms, our goal is to find a DAG with maximum score, where our scoring criterion could be the Bayesian score, the BIC score, or some other score. Therefore, we will simply refer to the score as score(G : D), where D is our data.

If we use either the Bayesian score or the BIC score, the score for the entire DAG is a product of local scores for each node. For example, Theorem 13.3 obtains the result that the Bayesian score is given by

```
P(\mathbf{D}|\mathbb{G}) = \prod_{i=1}^n \prod_{j=1}^{q_i^{\mathbb{G}}} \frac{\Gamma(N_{ij}^{\mathbb{G}})}{\Gamma(N_{ij}^{\mathbb{G}} + M_{ij}^{\mathbb{G}})} \frac{\Gamma(a_{ij}^{\mathbb{G}} + s_{ij}^{\mathbb{G}})\Gamma(b_{ij}^{\mathbb{G}} + t_{ij}^{\mathbb{G}})}{\Gamma(a_{ij}^{\mathbb{G}})\Gamma(b_{ij}^{\mathbb{G}})}.
```

See Theorem 13.33 for the definition of the variables in this formula. Note that we have now explicitly shown their dependence on G. Let PA_i^G denote the parents of X_i in G. For each node X_i, define

```
score(X_i, \mathbf{PA}_i^{\mathbb{G}} : \mathbf{D}) = \prod_{j=1}^{q_i^{\mathbb{G}}} \frac{\Gamma(N_{ij}^{\mathbb{G}})}{\Gamma(N_{ij}^{\mathbb{G}} + M_{ij}^{\mathbb{G}})} \frac{\Gamma(a_{ij}^{\mathbb{G}} + s_{ij}^{\mathbb{G}})\Gamma(b_{ij}^{\mathbb{G}} + t_{ij}^{\mathbb{G}})}{\Gamma(a_{ij}^{\mathbb{G}})\Gamma(b_{ij}^{\mathbb{G}})}.
```

This local score depends only on parameter values stored at X_i, and data values of X_i and nodes in PA_i^G, and the P(D|G) is the product of these local scores.

Cooper and Herskovits [1992] developed a greedy search algorithm that tries to maximize the score of the DAG by maximizing these local scores. That is, for each variable X_i, they locally find a value PA_i that approximately maximizes score(X_i, PA_i^G : D). The single operation in this search algorithm is the addition of a parent to a node. The algorithm proceeds as follows: We assume an ordering of the nodes such that if X_i precedes X_j in the ordering, an arc from X_j to X_i is not allowed. Let Pred(X_i) be the set of nodes that precede X_i in the ordering. We initially set the parents PA_i^G of X_i to empty and compute score(X_i, PA_i^G : D). Next we visit the nodes in sequence according to the ordering. When we visit X_i, we determine the node in Pred(X_i) that most increases score(X_i, PA_i^G : D). We “greedily” add this node to PA_i. We continue doing this until the addition of no node increases score(X_i, PA_i^G : D). Pseudocode for this algorithm follows. The algorithm is called K2 because it evolved from a system named Kutató [Herskovits and Cooper, 1990].