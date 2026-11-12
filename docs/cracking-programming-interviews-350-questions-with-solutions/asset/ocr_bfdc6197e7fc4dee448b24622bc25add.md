# Chapter 3

# Trees

# 3.1 Lowest Common Ancestor (LCA) Problem

# Problem

Find the lowest common ancestor (aka lca), i.e., ancestor with maximal depth, of a pair of nodes in a rooted tree.

# Solution

# Basic Analysis

In a rooted tree $T$, a node $u$ is an ancestor of a node $v$ if $u$ is on the unique path from the root to $v$. It can be easily inferred from this definition that a node is an ancestor of itself. A *proper ancestor* of $v$ refers to an ancestor that is not $v$.

In a rooted tree $T$, the *lowest common ancestor* (aka *lca*) of two nodes $x$ and $y$ is the deepest node in $T$ that is an ancestor of both $x$ and $y$. LCA problem is one of the most fundamental algorithmic problems on trees and it has been intensively studied mainly due to:

+   - It is inherently algorithmically beautiful.
+   - Fast algorithms for the LCA problem can be used to solve other algorithmic problems.

The set of ancestors $a(u)$ of a node $u \in V$ is defined as:

$$a(u)=\begin{cases}\{x\}\cup a(\operatorname{parent}(x)), & x\ne\operatorname{root}\\\{x\}, & \text{otherwise}\end{cases}$$

where $\operatorname{parent}(x)$ is the parent of a node $x$ in the tree.