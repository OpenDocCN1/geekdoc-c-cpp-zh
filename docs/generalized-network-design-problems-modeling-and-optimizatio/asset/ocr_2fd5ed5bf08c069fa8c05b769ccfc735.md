Offspring are produced from two parents, using the 2-point order standard crossover procedure, which creates offspring that preserves the order and position of symbols in a subsequence of one parent, while preserving the relative order of the remaining symbols from the other parent. It is implemented by selecting two random cut points which define the boundaries for a series of copying operations. First, the symbols between the cut points are copied from the first parent to the offspring. Then, starting just after the second cut point, the symbols are copied from the second parent to the offspring, omitting any symbols that were copied from the first parent. When the end of the second parent sequence is reached, this process continues with the first symbol of the second parent, until all symbols have been copied to the offspring. The second offspring is produced by swapping the parents and then using the same procedure.

Next, we present the application of the proposed 2-point order crossover in the case of the problem presented in Figure 5.7. We assume two well-structured parents, chosen at random, with the cutting points between nodes 2 and 3, respectively 5 and 6:

```
P₁ = 18 0 | 3 6 0 | 7 10 16
P₂ = 5 2 | 18 0 15 | 13 8
```

Note that the length of each individual differs according to the number of routes. According to Figure 5.7, the cluster representation of the previously selected parents is:

```
C₁ = 6 0 | 1 2 0 | 3 4 5
C₂ = 2 1 | 6 0 0 5 | 4 3
```

The sequences between the two cutting points are copied to the two offspring:

```
O₁ = x x | 3 6 0 | x x x
O₂ = x x | 18 0 15 | x x x
```

The nodes of parent P₁ are copied to the offspring O₂ if O₂ does not already contain nodes in the same clusters as the nodes of P₁. The sequence of nodes of P₁ is 18-0-3-6-0-7-10-16, and the clusters are 6-0-1-2-0-3-4-5. Note that cluster 6 is already represented in O₂ by node 18 and cluster by node 16. The depot (0) is kept anyway, since it is a splitter. Therefore, the remaining sequence of nodes in P₁ is 0-3-6-0-7-10.

```
O₂ = 0 3 | 18 0 15 | 6 0 7 10 .
```

Following this, the nodes of the parent P₂ are copied to the offspring O₁ in the same manner. The nodes of the clusters not present in O₁ are copied to the remaining positions:

```
O₁ = 18 0 | 3 6 0 | 15 13 8
```

# Mutation operators

The mutation operator is a genetic operator that alters one or more gene values in a chromosome from its initial state. This can result in entirely new gene values being