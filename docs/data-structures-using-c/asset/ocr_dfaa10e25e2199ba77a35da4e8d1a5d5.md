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

# Binary Tree With n Nodes Having n + 1 External Nodes

Taking the base case of a tree with only one node, that is the root, it has two external nodes or null links. So, if n = 1, then the number of external nodes is n + 1, that is, 2.
From this base case, if there are n internal nodes where the left subtree has L nodes, then the right subtree has n – L – 1 internal nodes (1 for the root).
By induction hypothesis, the number of external nodes of the left subtree is L + 1. The number of external nodes of the right subtree is (n – L – 1) + 1 = n – L. So, the total number of external nodes is L + 1 + n – L = n + 1.

# 7.4 BINARY TREE ABSTRACT DATA TYPE

We have defined a binary tree. Let us now define it as an abstract data type (ADT), which includes a list of operations that process it.

```
ADT btree
1. Declare create() → btree
2. maketree(btree, element, btree) → btree
3. isEmpty(btree) → boolean
4. leftchild(btree) → btree
5. rightchild(btree) → btree
6. data(btree) → element
7. for all l, r e tree, e e element, Let
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