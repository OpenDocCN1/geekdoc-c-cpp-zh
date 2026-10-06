# Creating a Tree Structure

A tree is a basic data structure in computer science. It is a hierarchy indicated by a tree-like structure that has some nodes within it. A typical tree structure is shown in Figure 7-11, and the sections that follow it describe variations in this structure.

![](bbox=[0.125, 0.161, 0.351, 0.36])

FIGURE 7-11 A tree structure

F# tree representation and traversal The F# representation of the tree structure in Figure 7-11 is shown in Listing 7-18. This structure is created with the help of a discriminated union (DU).

LISTING 7-18 Tree representation for the tree structure in Figure 7-11

```
type NodeType = int
// DU definition for a tree structure
type Tree =
| Node of NodeType * Tree list

let createTree() =
Node(1, [Node(2, [Node(4, []);]);
Node(5, [])]);
  Node(3, [Node(6, []);]);
Node(7, [Node(9, []))]);
Node(8, []])
])
```

Pre-order and post-order tree traversal are two basic tree operations. Pre-order traversal processes the tree from the current node and then processes subtrees starting from the root node. Post-order traversal processes the tree from the subtrees and then processes the current node starting from the root node. Listing 7-19 shows both processes.