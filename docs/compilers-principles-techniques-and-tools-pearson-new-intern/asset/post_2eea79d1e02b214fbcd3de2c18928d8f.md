
## 9.6. LOOPS IN FLOW GRAPHS

all but 1, 2 and 3, since all paths from 1 must begin with 1 → 2 → 3 → 4 or 1 → 3 → 4. Nodes 5 and 6 dominate only themselves, since flow of control can skip around either by going through the other. Finally, 7 dominates 7, 8, 9, and 10; 8 dominates 8, 9, and 10; 9 and 10 dominate only themselves.

![](img/a29d16e454785bb105e96ef448ac07f6_661_0.png)

Figure 9.38: A flow graph

A useful way of presenting dominator information is in a tree, called the *dominator tree*, in which the entry node is the root, and each node *d* dominates only its descendants in the tree. For example, Fig. 9.39 shows the dominator tree for the flow graph of Fig. 9.38.

![](img/a29d16e454785bb105e96ef448ac07f6_661_1.png)

Figure 9.39: Dominator tree for flow graph of Fig. 9.38

The existence of dominator trees follows from a property of dominators: each node *n* has a unique *immediate dominator* *m* that is the last dominator of *n* on any path from the entry node to *n*. In terms of the *dom* relation, the

### Properties of the *dom* Relation

A key observation about dominators is that if we take any acyclic path from the entry to node *n*, then all the dominators of *n* appear along this path, and moreover, they must appear in the same order along any such path. To see why, suppose there were one acyclic path *P*₁ to *n* along which dominators *a* and *b* appeared in that order and another path *P*₂ to *n*, along which *b* preceded *a*. Then we could follow *P*₁ to *a* and *P*₂ to *n*, thereby avoiding *b* altogether. Thus, *b* would not really dominate *n*.

This reasoning allows us to prove that *dom* is transitive: if *a dom b* and *b dom c*, then *a dom c*. Also, *dom* is antisymmetric: it is never possible that both *a dom b* and *b dom a* hold, if *a* ≠ *b*. Moreover, if *a* and *b* are two dominators of *n*, then either *a dom b* or *b dom a* must hold. Finally, it follows that each node *n* except the entry must have a unique immediate dominator — the dominator that appears closest to *n* along any acyclic path from the entry to *n*.

*D*(2) = {2} ∪ *D*(1). Thus, *D*(2) is set to {1, 2}. Then node 3, with predecessors 1, 2, 4, and 8, is considered. Since all the interior nodes are initialized with the universal set *N*,

*D*(3) = {3} ∪ ({1} ∩ {1, 2} ∩ {1, 2, …, 10} ∩ {1, 2, …, 10}) = {1, 3}

The remaining calculations are shown in Fig. 9.41. Since these values do not change in the second iteration through the outer loop of lines (3) through (6) in Fig. 9.23(a), they are the final answers to the dominator problem. □

*D*(4) = {4} ∪ (*D*(3) ∩ *D*(7)) = {4} ∪ ({1, 3} ∩ {1, 2, …, 10}) = {1, 3, 4}  
*D*(5) = {5} ∪ *D*(4) = {5} ∪ {1, 3, 4} = {1, 3, 4, 5}  
*D*(6) = {6} ∪ *D*(4) = {6} ∪ {1, 3, 4} = {1, 3, 4, 6}  
*D*(7) = {7} ∪ (*D*(5) ∩ *D*(6) ∩ *D*(10))  
    = {7} ∪ ({1, 3, 4, 5} ∩ {1, 3, 4, 6} ∩ {1, 2, …, 10}) = {1, 3, 4, 7}  
*D*(8) = {8} ∪ *D*(7) = {8} ∪ {1, 3, 4, 7} = {1, 3, 4, 7, 8}  
*D*(9) = {9} ∪ *D*(8) = {9} ∪ {1, 3, 4, 7, 8} = {1, 3, 4, 7, 8, 9}  
*D*(10) = {10} ∪ *D*(8) = {10} ∪ {1, 3, 4, 7, 8} = {1, 3, 4, 7, 8, 10}

Figure 9.41: Completion of the dominator calculation for Example 9.39

### 9.6.2  Depth-First Ordering

As introduced in Section 2.3.4, a *depth-first search* of a graph visits all the nodes in the graph once, by starting at the entry node and visiting the nodes as far away from the entry node as quickly as possible. The route of the search in a depth-first search forms a *depth-first spanning tree* (DFST). Recall from Section 2.3.4 that a preorder traversal visits a node before visiting any of its children, which it then visits recursively in left-to-right order. Also, a postorder traversal visits a node’s children, recursively in left-to-right order, before visiting the node itself.

There is one more variant ordering that is important for flow-graph analysis: a *depth-first ordering* is the reverse of a postorder traversal. That is, in a depth-first ordering, we visit a node, then traverse its rightmost child, the child to its left, and so on. However, before we build the tree for the flow graph, we have choices as to which successor of a node becomes the rightmost child in the tree, which node becomes the next child, and so on. Before we give the algorithm for depth-first ordering, let us consider an example.

**Example 9.40:** One possible depth-first presentation of the flow graph in Fig. 9.38 is illustrated in Fig. 9.42. Solid edges form the tree; dashed edges are the other edges of the flow graph. A depth-first traversal of the tree is given by: 1 → 3 → 4 → 6 → 7 → 8 → 10, then back to 8, then to 9. We go back to 8 once more, retreating to 7, 6, and 4, and then forward to 5. We retreat from 5 back to 4, then back to 3 and 1. From 1 we go to 2, then retreat from 2, back to 1, and we have traversed the entire tree.

The preorder sequence for the traversal is thus

1, 3, 4, 6, 7, 8, 10, 9, 5, 2.

The postorder sequence for the traversal of the tree in Fig. 9.42 is

10, 9, 8, 7, 6, 5, 4, 3, 2, 1.

The depth-first ordering, which is the reverse of the postorder sequence, is

1, 2, 3, 4, 5, 6, 7, 8, 9, 10.

We now give an algorithm that finds a depth-first spanning tree and a depth-first ordering of a graph. It is this algorithm that finds the DFST in Fig. 9.42 from Fig. 9.38.

**Algorithm 9.41:** Depth-first spanning tree and depth-first ordering.

**INPUT:** A flow graph *G*.

**OUTPUT:** A DFST *T* of *G* and an ordering of the nodes of *G*.

![](img/a29d16e454785bb105e96ef448ac07f6_665_0.png)

Figure 9.42: A depth-first presentation of the flow graph in Fig. 9.38

**METHOD:** We use the recursive procedure *search(n)* of Fig. 9.43. The algorithm initializes all nodes of *G* to “unvisited,” then calls *search(n₀)*, where *n₀* is the entry. When it calls *search(n)*, it first marks *n* “visited” to avoid adding *n* to the tree twice. It uses *c* to count from the number of nodes of *G* down to 1, assigning depth-first numbers *dfn[n]* to nodes *n* as we go. The set of edges *T* forms the depth-first spanning tree for *G*. □

**Example 9.42:** For the flow graph in Fig. 9.42, Algorithm 9.41 sets *c* to 10 and begins the search by calling *search(1)*. The rest of the execution sequence is shown in Fig. 9.44. □

### 9.6.3 Edges in a Depth-First Spanning Tree

When we construct a DFST for a flow graph, the edges of the flow graph fall into three categories.

- 1. There are edges, called *advancing edges*, that go from a node *m* to a proper descendant of *m* in the tree. All edges in the DFST itself are advancing edges. There are no other advancing edges in Fig. 9.42, but, for example, if 4 → 8 were an edge, it would be in this category.
- 2. There are edges that go from a node *m* to an ancestor of *m* in the tree (possibly to *m* itself). These edges we shall term *retreating edges*. For example, 4 → 3, 7 → 4, 10 → 7, 8 → 3, and 9 → 1 are the retreating edges in Fig. 9.42.

```text
void search(n) {
    mark n “visited”;
    for (each successor s of n)
        if (s is “unvisited”) {
            add edge n → s to T;
            search(s);
        }
    dfn[n] = c;
    c = c − 1;
}

main() {
    T = ∅; /* set of edges */
    for (each node n of G)
        mark n “unvisited”;
        c = number of nodes of G;
        search(n₀);
}
```

Figure 9.43: Depth-first search algorithm

- 3. There are edges *m* → *n* such that neither *m* nor *n* is an ancestor of the other in the DFST. Edges 2 → 3 and 5 → 7 are the only such examples in Fig. 9.42. We call these edges *cross edges*. An important property of cross edges is that if we draw the DFST so children of a node are drawn from left to right in the order in which they were added to the tree, then all cross edges travel from right to left.

It should be noted that *m* → *n* is a retreating edge if and only if *dfn[m]* ≥ *dfn[n]*. To see why, note that if *m* is a descendant of *n* in the DFST, then search(*m*) terminates before search(*n*), so *dfn[m]* ≥ *dfn[n]*. Conversely, if *dfn[m]* ≥ *dfn[n]*, then search(*n*) terminates before search(*m*), or *m* = *n*. But search(*n*) must have begun before search(*m*) if there is an edge *m* → *n*, or else the fact that *n* is a successor of *m* would have made *n* a descendant of *m* in the DFST. Thus the time search(*m*) is active is a subinterval of the time search(*n*) is active, from which it follows that *n* is an ancestor of *m* in the DFST.

### 9.6.4  Back Edges and Reducibility

A *back edge* is an edge *a* → *b* whose head *b* dominates its tail *a*. For any flow graph, every back edge is retreating, but not every retreating edge is a back edge. A flow graph is said to be *reducible* if all its retreating edges in any depth-first spanning tree are also back edges. In other words, if a graph is reducible, then all the DFST’s have the same set of retreating edges, and
