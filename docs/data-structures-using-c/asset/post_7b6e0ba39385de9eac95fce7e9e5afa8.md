
## Definition A binary tree

- 1. is either an empty tree or
- 2. consists of a node, called root, and two children, left and right, each of which is itself a binary tree.

The definition is recursive as we have defined a binary tree in terms of itself. All the internal nodes of a binary tree are themselves the roots of smaller binary trees (Fig. 7.21).

![img/a99ec79093c067f0bed8f1086197950e_305_0.png]

Fig. 7.21 Binary tree

Let us consider the two distinct binary trees in Fig. 7.22.

![img/a99ec79093c067f0bed8f1086197950e_305_1.png]

Fig. 7.22 Two binary trees

The definition implies that every non-empty node has two children, either of which may be empty. Here A's right child and B's left child are empty trees (represented by shaded boxes). Usually, empty trees in a binary tree are not shown.

## 7.3.1 Properties of a Binary Tree

A tree is a connected acyclic graph. In many ways, a tree is the simplest non-trivial type of graph. It has several good properties such as the fact that there exists a unique path between every two vertices. The following theorems list some simple properties of trees:

Let T be a tree. Then the following properties hold true:

- 1. There exists a unique path between every two vertices.
- 2. The number of vertices is one more than the number of edges in the tree.
- 3. A tree with two or more vertices has at least two leaves.

Let us refer to Fig. 7.23 for proving these properties.

![img/a99ec79093c067f0bed8f1086197950e_306_0.png]

Fig. 7.23 Binary trees (a) Sample 1 (b) Sample 2

### Property 1

Property 1 comes from the definition of a tree. As a tree is a connected graph, there exists at least one path between every two vertices. However, if there are two or more paths between a pair of vertices, there would be a circuit in the graph and so the graph cannot be a tree.

### Property 2

Property 2 can be proved using mathematical induction. Let there be a tree T with the total number of edges e and the total number of vertices v.

### Induction step

A tree with one vertex contains no edge, and a tree with two vertices has one edge.

### Induction hypothesis

Let us consider that there is an edge {a, b} in T such that the removal of the edge {a, b} divides T into two disjoint trees T1 and T2, where T1 contains the vertex a and all the vertices whose paths to a in T do not contain the edge {a, b}, and T2 contains the vertex b and all the vertices whose paths to b do not contain the edge {a, b}.

Since both T1 and T2 have at most v - 1 vertices, it follows from the hypothesis that

```
for T1 => e1 = v1 - 1 and
for T2 => e2 = v2 - 1,
```

where e1 and e2 are the number of edges and v1 and v2 are the number of vertices in T1 and T2, respectively.

Thus e1 + e2 = v1 + v2 - 2

Since \( e = e_1 + e_2 + 1 \) and \( v = v_1 + v_2 \), we have \( e = v - 1 \), as shown in the following figure:

![img/a99ec79093c067f0bed8f1086197950e_307_0.png]

### Property 3

Property 3 follows from Property 2, that is, the sum of degrees of the vertices in any graph is equal to 2e, which is equal to 2v - 2, in a tree. Since a tree with more than one vertex cannot have any isolated vertex, there must be at least two vertices of indegree 1 in the tree.

### Other Properties

- 1. The maximum number of nodes of level \( i \) in a binary tree is \( 2^{i-1} \), where \( i \ge 1 \).
- 2. The maximum number of nodes of depth \( d \) in a binary tree is \( 2^{d-1} \), where \( d \ge 1 \).

Let us prove these properties using induction. Assume the root is only one node at level 1.

Hence, the maximum number of nodes is \( 2^{i-1} \), that is, \( 2^{1-1} = 2^0 = 1 \).

By induction hypothesis, let \( i \) be any arbitrary positive integer greater than 1. Then, the maximum number of nodes on level \( i - 1 \) is \( 2^{i-2} \).

Hence, it is proved that the maximum number of nodes at level \( i \) is \( 2^{i-1} \).

Note: If we assume the root at level 0, then the expression is \( 2^i \).

Since each node in a binary tree has a maximum degree 2, the maximum number of nodes at level \( i \) is \( 2^{i-1} \).

The maximum number of nodes of depth \( d \) of a binary tree is given by

\( \sum_{i=1}^{d} (\text{maximum no. of nodes at level } i) = \sum_{i=1}^{d} 2^{i-1} \)

### Relation Between Number of Leaf Nodes and Degree-2 Nodes

In any non-empty tree T, if there are \( n_0 \) leaf nodes and \( n_2 \) nodes of degree 2, then

\( n_0 = n_2 + 1 \)

Let \( n_1 \) be the number of nodes of degree 1 and \( n \) be the total number of nodes.

Since all nodes in \( T \) are of at most degree 2, then

\( n = n_0 + n_1 + n_2 \) (7.1)

If the number of branches is B, then n = B + 1. For a binary tree, all the branches stem out from a node of degree 1 or 2. Thus,

```
B = n₁ + 2 n₂
So, n = B + 1
B = n₁ + 2 × n₂ + 1
(7.2)
```

Subtracting Eq. (7.2) from Eq. (7.1) we get

```
n₀ = n₂ + 1
```

### Binary Tree With n Nodes Having n + 1 External Nodes

Taking the base case of a tree with only one node, that is the root, it has two external nodes or null links. So, if n = 1, then the number of external nodes is n + 1, that is, 2.
From this base case, if there are n internal nodes where the left subtree has L nodes, then the right subtree has n – L – 1 internal nodes (1 for the root).
By induction hypothesis, the number of external nodes of the left subtree is L + 1. The number of external nodes of the right subtree is (n – L – 1) + 1 = n – L. So, the total number of external nodes is L + 1 + n – L = n + 1.

## 7.4 BINARY TREE ABSTRACT DATA TYPE

We have defined a binary tree. Let us now define it as an abstract data type (ADT), which includes a list of operations that process it.

```
ADT btree
1. Declare create() → btree
2. maketree(btree, element, btree) → btree
3. isEmpty(btree) → boolean
4. leftchild(btree) → btree
5. rightchild(btree) → btree
6. data(btree) → element
7. for all l, r ∈ tree, e ∈ element, Let
8. isEmpty(create()) = true
9. isEmpty(maketree(l, e, r)) = false
10. leftchild(create()) = error
11. rightchild(create()) = error
12. leftchild(maketree(l, e, r)) = l
13. rightchild(maketree(l, e, r)) = r
14. data(maketree(l, e, r)) = e
15. end
end btree
```

The six functions with their domains and ranges are declared in lines 1 through 6. Lines 7 through 14 are the set of axioms that describe how the functions are related.

The create() operation creates an empty binary tree; the isEmpty() operation checks whether btree is empty or not and returns the Boolean value true or false, respectively; leftChild(btree) and rightChild(btree) return the left and right subtrees, respectively; data(btree) returns the data element. Program Code 7.1 states the class definition of the operations that process the tree ADT.

```
PROGRAM CODE 7.1
class TreeNode
{
    public:
    char Data;
    TreeNode *LChild;
    TreeNode *RChild;
};

class BinaryTree
{
    private:
    TreeNode *Root;
    public:
    BinaryTree() {Root = NULL};
    // constructor creates an empty tree
    TreeNode * GetNode();
    void InsertNode( TreeNode* );
    void DeleteNode( TreeNode* );
};
```

### Operations on binary tree

The basic operations on a binary tree can be as listed as follows:

- 1. Creation—Creating an empty binary tree to which the 'root' points
- 2. Traversal—Visiting all the nodes in a binary tree
- 3. Deletion—Deleting a node from a non-empty binary tree
- 4. Insertion—Inserting a node into an existing (may be empty) binary tree
- 5. Merge—Merging two binary trees
- 6. Copy—Copying a binary tree
- 7. Compare—Comparing two binary trees
- 8. Finding a replica or mirror of a binary tree

## 7.5 REALIZATION OF A BINARY TREE

In this section, we shall study the basic realization of a binary tree and discuss its capabilities for supporting various operations. The implementation of a binary tree should represent the hierarchical relationship between a parent node and its left and right children. We have studied the elementary data structures such as linked list and arrays. Now, we shall extend these concepts to the binary tree structures. We shall give more emphasis to the linked implementation as it is more popular than the corresponding sequential structure due to the following two main reasons:

- 1. A binary tree has a natural implementation in a linked storage.
- 2. The linked structure is more convenient for insertions and deletions.

Let us study both the implementations.

### 7.5.1 Array Implementation of Binary Trees

One of the ways to represent a tree using an array is to store the nodes level-by-level, starting from the level 0 where the root is present. Such a representation requires sequential numbering of the nodes, starting with nodes on level 0, then those on level 1, and so on.

We have defined a complete tree. A complete binary tree of height h has (2^(h+1) - 1) nodes in it. The nodes can be stored in a one-dimensional array, tree, with the node numbered at the location tree(i). An array of size 2^(h+1) - 1 is needed for the same.

The root node is stored in the first memory location as the first element in the array. The following rules can be used to decide the location of any i^th node of a tree: For any node with index i, 0 <= i <= n - 1,

- 1. Parent(i) = floor((i - 1)/2) if i != 0; if i = 0, then it is the root that has no parent.
- 2. Lchild(i) = 2 * i + 1 if 2i + 1 <= n - 1; if 2i >= n, then i has no left child.
- 3. Rchild(i) = 2i + 2 if 2i + 2 <= n - 1; if (2i + 1) >= n, then i has no right child.

Let us consider the complete binary tree in Fig. 7.24.

![img/a99ec79093c067f0bed8f1086197950e_310_0.png]

Fig. 7.24 Complete binary tree

The representation of binary tree in Fig. 7.24 using an array is as follows:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|---|
| A | B | E | C | D | F | G | - | - |

Let us consider one more example as in Fig. 7.25.
