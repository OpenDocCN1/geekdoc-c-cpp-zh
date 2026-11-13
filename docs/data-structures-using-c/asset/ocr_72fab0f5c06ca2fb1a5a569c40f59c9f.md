assign a code that is a sequence of labels of the edges in the path from the root to that of leaf (Fig. 7.82).

![](bbox=[0.385, 0.163, 0.715, 0.361])

# Fig. 7.82 Prefix codes

It is always possible to divide a received sequence of 0s and 1s into the sequences that are in a prefix code. Starting at the root of the binary tree, we shall trace a downward path in the tree according to the bits in the received sequence. At a branch node, we shall follow the edge labelled with 0 if we encounter a 0 in the received sequence, and we shall follow the edge labelled with a 1 if we encounter a 1 in the received sequence. When the downward path reaches a leaf, it shows that the prefix code has been detected. For the next sequence, we should return to the root of the tree. This process clearly assures that the variable length code, which is the prefix code, has no ambiguity.

Now the problem is about constructing a binary tree. Suppose we are given a set of weights w1, w2, ..., wn. Let us assume that w1 ≤ w2 ≤ ... ≤ wn. A binary tree that has n leaves with weights w1, w2, ..., wn assigned to the leaves is called a binary tree for weight w1, w2, ..., wn. Our aim is to assign smaller code to the leaf of higher weights, as the weights here denote the frequency of occurrence. The length of sequence of bits assigned to a leaf node is path length of that node. Hence, we want lesser path length to the leaf nodes with higher weights.

Let the weight of a tree T be denoted by w(T). The weight of a binary tree for weights w1, w2, ..., wn is given by

```
w(T) = \sum_{i=1}^n w_i L(w_i), where

L(w_i) = path length of node of weight w_i.
```

A binary tree for weights w1, w2, ..., wn is said to be an optimal binary tree if its weight is minimum. Hence, our aim is to construct a tree such that w(T) is minimum.