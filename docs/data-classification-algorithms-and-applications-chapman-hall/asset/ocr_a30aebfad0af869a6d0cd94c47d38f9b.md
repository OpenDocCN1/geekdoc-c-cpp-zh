![](bbox=[0.15, 0.07, 0.82, 0.32])

FIGURE 2.8: An illustration of the graph of 7 features {f1, f2, …, f7} and its corresponding representation A.

# 2.3.3 Features with Graph Structure

We often have knowledge about pair-wise dependencies between features in many real-world applications [58]. For example, in natural language processing, digital lexicons such as WordNet can indicate which words are synonyms or antonyms; many biological studies have suggested that genes tend to work in groups according to their biological functions, and there are some regulatory relationships between genes. In these cases, features form an undirected graph, where the nodes represent the features, and the edges imply the relationships between features. Several recent studies have shown that the estimation accuracy can be improved using dependency information encoded as a graph.

Let G(N, E) be a given graph where N = {1, 2, …, m} is a set of nodes, and E is a set of edges. Node i corresponds to the i-th feature and we use A ∈ R^{m×m} to denote the adjacency matrix of G. Figure 2.8 shows an example of the graph of 7 features {f1, f2, …, f7} and its representation A.

If nodes i and j are connected by an edge in E, then the i-th feature and the j-th feature are more likely to be selected together, and they should have similar weights. One intuitive way to formulate graph Lasso is to force weights of two connected features close by a square loss as

```
penalty(w, G) = λ||w||₁ + (1 − λ) Σ_{i,j} A_{ij} (w_i − w_j)², (2.26)
```

which is equivalent to

```
penalty(w, G) = λ||w||₁ + (1 − λ) wᵀ L w, (2.27)
```

where L = D − A is the Laplacian matrix and D is a diagonal matrix with D_{ii} = Σ_{j=1}^m A_{ij}. The Laplacian matrix is positive semi-definite and captures the underlying local geometric structure of the data. When L is an identity matrix, wᵀ L w = ||w||₂² and then Equation (2.27) reduces to the elastic net penalty [81]. Because wᵀ L w is both convex and differentiable, existing efficient algorithms for solving the Lasso can be applied to solve Equation (2.27).