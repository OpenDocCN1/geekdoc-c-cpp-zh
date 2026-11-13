
than one expression trees with same infix form.

![](img/723fa3ef35f5102eb67dc45b74bb823d_187_0.png)

Figure 8.7: Expression Tree of infix expression A + B * C

Table 8.1: Different forms of expression

| Expression | Prefix form | Infix form | Postfix form |
|---|---|---|---|
| A + (B * C) | + A*BC | A + B * C | ABC*+ |
| (A + B) * C | *+ABC | A + B * C | AB+C* |

## Construction of Expression Tree

An expression can be converted to its equivalent postfix expression. The following algorithm constructed an expression tree from a valid postfix expression P containing binary operators:

## Algorithm to create expression tree

```
Algorithm: CREATE_EXPRESSION_TREE (P)
1. Repeat while not the end of the expression P
2. Read the postfix expression one symbol S at a time
3. If S is an operand then
   i) Create a node for the operand
  ii) Push the pointer to the created node onto a stack
4. If S is a binary operator then
   i) Create a node for the operator
  ii) T1 = Pop from the stack a pointer to an operand
 iii) T2 = Pop from the stack a pointer to an operand
  iv) Make T2 the left subtree and T1 the right subtree of the operator node
   v) Push the pointer to the operator node onto the stack
 [End of while]
5. T = Pop from the stack a pointer to expression tree
6. Return
```

## Example

Draw a expression tree from the following expression:

A * B ^ C / D + E

Now, at first converts the above expression to its equivalent postfix expression: A B C ^ * D / E +

![](img/723fa3ef35f5102eb67dc45b74bb823d_188_0.png)

Figure 8.8: Expression Tree

The preorder traversal of the above expression tree is + / * A B C D E, this is the prefix form of the expression. The postorder traversal of the above expression tree is A B C ^ * D / E +, this is the postfix form of the expression.

## Evaluation of Expression Tree

A postfix expression can be converted to expression tree using the above algorithm. Now we can evaluate the expression tree, using the following algorithm:

## Algorithm: evaluation of expression tree

```
ALGORITHM: EVALUATION (T)
1. If T is a leaf then
2. Return value of T's operand
3. Else
4. Operator = T.Element
5. Operand1 = EVALUATION(T.Left)
6. Operand2 = EVALUATION(T.Right)
7. Return (Operation (Operand1, Operator, Operand2))
8. [End of If]
End
```

## Balanced Binary Tree

There are mainly two types of balanced binary trees.

- i) Weight balanced binary tree
- ii) Height balanced binary tree

## Weight Balanced Binary Tree

A weight-balanced binary tree is a binary search tree if for each node it holds that the number of inner nodes in the left subtree and the number of inner nodes in the right subtree differ by at most one. These trees can be used to implement dynamic sets, dictionaries (maps) and sequences. The weight-balanced binary trees were introduced by Nievergelt and Reingold in 1972. It is purely functional implementations are widely used in functional programming languages.

## Height Balanced Binary Tree

A height-balanced binary tree has the minimum height for the leaf nodes. A binary tree is height balanced if height of the tree is O (log n) where n is number of nodes. One common height-balanced tree structure is a binary tree structure in which the left and right subtrees of every node differ in height by no more than one.

For Example, AVL Tree (Adel'son-Vel'skii and E. M. Landis, 1962) maintain O (log n) height by making sure that the difference between heights of left and right subtrees is at most ±1. Red-Black trees (Guibas and Sedgewick, 1978) maintain O (log n) height by making sure that the number of Black nodes on every root to leaf paths are same and there is no adjacent red nodes. Balanced Binary Search trees are performed good as they provide O (log n) time for search, insert and delete operations.

## Threaded Binary Tree

A threaded binary tree is a binary tree in which having a loop. In a binary tree, most of the entries in the link field will contain null elements. These null entries are replaced by special pointers, which point to nodes higher in the tree. These special pointers are called threads and binary trees with such pointers are called threaded tree.

- For a n-node binary tree, there exists
  - total n2 number of pointer or link fields
  - total n-1 number of actual (not null) pointers or link fields
  - total n+1 number of null pointers or link fields

For optimizing null pointers, the concept of the thread is used. There are different types of threaded binary trees are possible, inorder threaded binary trees, preorder threaded binary trees, and postorder threaded binary trees correspond to inorder, preorder and postorder traversals. Each type of threaded binary trees can be of two representations: one-way threading and two-way threading.

![](img/723fa3ef35f5102eb67dc45b74bb823d_189_0.png)

Figure 8.9: One-way inorder threaded binary tree

In the one-way inorder threaded binary tree, an only right null pointer used as a thread that will point to the next node in the inorder traversal (i.e. inorder successor). However, the right null pointer of the last node remains unused. In the two-way inorder threaded binary tree, left null pointer acts as a thread that will point to the previous node in the inorder traversal (i.e. inorder predecessor) and right null pointer acts as a thread that will point to the next node in the inorder traversal (i.e. inorder successor). However, the left null pointer of the first node and the right null pointer of the last node remains unused.

![](img/723fa3ef35f5102eb67dc45b74bb823d_190_0.png)

Figure 8.10: Two-way inorder threaded binary tree

The structure definition for a node of two-way inorder threaded binary tree as follows:

```c
struct Node
{
    struct Node *left;
    char lthread;
    int info;
    struct Node *right;
    char rthread;
};
typedef struct Node ThreadedTreeNode;
```

## Properties of Binary Tree

### Lemma 1

A binary tree with n nodes has exactly n – 1 edges (same as any normal tree).

**Proof:** The property can be proof by induction. **Induction Base:** Let n = 1. That is there is only one node in the tree. Therefore, a number of the edge is 0. Hence, the property is true for one node. **Induction Hypothesis:** Assume the property is true for n = k i.e., for k nodes there is k – 1 edges. **Induction Step:** The number of edges for k nodes is k - 1 edges by the induction hypothesis. Now addition of one node (i.e. n = k + 1) includes one extra edge. Therefore, total number of edges are = (k – 1) + 1 = k. Hence proved.

### Lemma 2

The maximum number of nodes on level i of a binary tree is 2^(i-1), i >= 1

**Proof:** The property can be proof by induction on i. **Induction Base:** The root is the only node on level i=1. Hence the maximum number of nodes on level = 1 is 2^0 = 2^(1-1). **Induction Hypothesis:** For all j, 1 <= j <= i, the maximum number of nodes on level j is 2^(j-1). **Induction Step:** The maximum number of nodes on level i-1 is 2^(i-2), by the induction hypothesis. Since each node in a binary tree has maximum degree 2, the maximum number of nodes on level i is two times the maximum number on level i-1, i.e. 2*2^(i-2) = 2^(i-1).

### Lemma 3

The maximum number of nodes in a binary tree of depth k is 2^(k+1), k>=1.

**Proof:** The maximum number of nodes on level i of a binary tree is 2^(i-1). Therefore, the maximum number of nodes in a binary tree of depth k is,

```
= \sum_{i=1}^k (maximum number of nodes on level i)
= \sum_{i=1}^k (2^{i-1})
= 2^{k+1} - 1
```

### Lemma 4

For any non-empty binary tree T, if n0 is the number of leaves (terminal nodes) and n2 be the number of nodes having degree 2 then n0 = n2 + 1.

**Proof:** Let n1, be the number of nodes of degree 1 and n is the total number of nodes. Since all the nodes in T are of degree <= 2 we have,

```
n = n0 + n1 + n2 (i)
```

Now, if we count the number of branches in a binary tree, we see that every node except for the root has a branch leading into it. If B is the number of branches, then n = B + 1. All the branches come either from a node of degree one or from a node of degree two. Thus, B = n1 + 2n2. Hence, we obtain

```
n = 1 + n1 + 2n2 (ii)
```

Subtracting (ii) from (i) and rearranging terms we get

```
n0 = n2 + 1
```

### Lemma 5

If n is the total number of nodes in a complete binary tree of height h, then h = [log2 n] + 1.

**Proof:** From the definition of a complete binary tree of height h, it is filled up to height h - 1 and in the last level, it may have partially filled with nodes. Hence, we can write:

```
2^(h-1) - 1 < n <= 2^h - 1
```

Since the maximum number of nodes at height h-1 is 2^(h-1) - 1 and at height, h is 2^h - 1.

```
or we can write 2^(h-1) <= n < 2^h (iii)
```

Taking the logarithm of (ii) we get

```
h - 1 < log2 n <= h
```

Therefore, the value of log2 n lies between h and h-1. Now if we take floor value of log2 n then it will be h-1.

Hence, h = [log2 n] + 1

## Representation of Binary Tree

Tree is a widely used abstract data type since it is defined in terms of operations on it and its implementation is hidden. Therefore, we can implement a tree using either array or linked list. Binary Tree also can be representation with two different ways.

- i) Using array
- ii) Using linked list
