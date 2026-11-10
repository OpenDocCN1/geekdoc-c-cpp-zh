
## 9.6. LOOPS IN FLOW GRAPHS

> **A Reason for Nonreducible Flow Graphs**
> 
> There is one place where we cannot generally expect a flow graph to be reducible. If we reverse the edges of a program flow graph, as we did in Algorithm 9.46 to find natural loops, then we may not get a reducible flow graph. The intuitive reason is that, while typical programs have loops with single entries, such loops sometimes have several exits, which become entries when we reverse the edges.

block ordering is actually two plus the depth. A study[^10] has shown that typical flow graphs have an average depth around 2.75. Thus, the algorithm converges very quickly.

[^10]: D. E. Knuth, “An empirical study of FORTRAN programs,” *Software—Practice and Experience* 1:2 (1971), pp. 105–133.

In the case of backward-flow problems, like live variables, we visit the nodes in the reverse of the depth-first order. Thus, we may propagate a use of a variable in block 17 backwards along the path

3 → 5 → 19 → 35 → 16 → 23 → 45 → 4 → 10 → 17

in one pass to IN[4], where we must wait for the next pass in order to reach OUT[45]. On the second pass it reaches IN[16], and on the third pass it goes from OUT[35] to OUT[3].

In general, one-plus-the-depth passes suffice to carry the use of a variable backward, along any acyclic path. However, we must choose the reverse of depth-first order to visit the nodes in a pass, because then, uses propagate along any decreasing sequence in a single pass.

The bound described so far is an upper bound on all problems where cyclic paths add no information to the analysis. In special problems such as dominators, the algorithm converges even faster. In the case where the input flow graph is reducible, the correct set of dominators for each node is obtained in the first iteration of a data-flow algorithm that visits the nodes in depth-first ordering. If we do not know that the input is reducible ahead of time, it takes an extra iteration to determine that convergence has occurred.

### 9.6.8 Exercises for Section 9.6

**Exercise 9.6.1:** For the flow graph of Fig. 9.10 (see the exercises for Section 9.1):

- i. Compute the dominator relation.
- ii. Find the immediate dominator of each node.
- iii. Construct the dominator tree.
- iv. Find one depth-first ordering for the flow graph.
- v. Indicate the advancing, retreating, cross, and tree edges for your answer to iv.
- vi. Is the flow graph reducible?
- vii. Compute the depth of the flow graph.
- viii. Find the natural loops of the flow graph.

**Exercise 9.6.2:** Repeat Exercise 9.6.1 on the following flow graphs:

- a) Fig. 9.3.
- b) Fig. 8.9.
- c) Your flow graph from Exercise 8.4.1.
- d) Your flow graph from Exercise 8.4.2.

! **Exercise 9.6.3:** Prove the following about the *dom* relation:

- a) If a *dom* b and b *dom* c, then a *dom* c (*transitivity*).
- b) It is never possible that both a *dom* b and b *dom* a hold, if a ≠ b (*antisymmetry*).
- c) If a and b are two dominators of n, then either a *dom* b or b *dom* a must hold.
- d) Each node n except the entry has a unique *immediate dominator* — the dominator that appears closest to n along any acyclic path from the entry to n.

! **Exercise 9.6.4:** Figure 9.42 is one depth-first presentation of the flow graph of Fig. 9.38. How many other depth-first presentations of this flow graph are there? Remember, order of children matters in distinguishing depth-first presentations.

!! **Exercise 9.6.5:** Prove that a flow graph is reducible if and only if when we remove all the back edges (those whose heads dominate their tails), the resulting flow graph is acyclic.

! **Exercise 9.6.6:** A *complete flow graph* on n nodes has arcs i → j between any two nodes i and j (in both directions). For what values of n is this graph reducible?

! **Exercise 9.6.7:** A *complete, acyclic flow graph* on n nodes 1, 2, . . . , n has arcs i → j for all nodes i and j such that i < j. Node 1 is the entry.

- a) For what values of *n* is this graph reducible?
- b) Does your answer to (a) change if you add self-loops *i* → *i* for all nodes *i*?

! **Exercise 9.6.8:** The natural loop of a back edge *n* → *h* was defined to be *h* plus the set of nodes that can reach *n* without going through *h*. Show that *h* dominates all the nodes in the natural loop of *n* → *h*.

!! **Exercise 9.6.9:** We claimed that the flow graph of Fig. 9.45 is nonreducible. If the arcs were replaced by paths of disjoint sets of nodes (except for the endpoints, of course), then the flow graph would still be nonreducible. In fact, node 1 need not be the entry; it can be any node reachable from the entry along a path whose intermediate nodes are not part of any of the four explicitly shown paths. Prove the converse: that every nonreducible flow graph has a subgraph like Fig. 9.45, but with arcs possibly replaced by node-disjoint paths and node 1 being any node reachable from the entry by a path that is node-disjoint from the four other paths.

!! **Exercise 9.6.10:** Show that every depth-first presentation for every nonreducible flow graph has a retreating edge that is not a back edge.

!! **Exercise 9.6.11:** Show that if the following condition

\[
f(a) \land g(a) \land a \leq f(g(a))
\]

holds for all functions *f* and *g*, and value *a*, then the general iterative algorithm, Algorithm 9.25, with iteration following a depth-first ordering, converges within 2-plus-the-depth passes.

! **Exercise 9.6.12:** Find a nonreducible flow graph with two different DFST’s that have different depths.

! **Exercise 9.6.13:** Prove the following:

- a) If a definition *d* is in IN[*B*], then there is some acyclic path from the block containing *d* to *B* such that *d* is in the IN’s and OUT’s all along that path.
- b) If an expression *x* + *y* is *not* available at the entrance to block *B*, then there is some acyclic path that demonstrates that fact; either the path is from the entry node and includes no statement that kills or generates *x* + *y*, or the path is from a block that kills *x* + *y* and along the path there is no subsequent generation of *x* + *y*.
- c) If *x* is live on exit from block *B*, then there is an acyclic path from *B* to a use of *x*, along which there are no definitions of *x*.

## 9.7 Region-Based Analysis

The iterative data-flow analysis algorithm we have discussed so far is just one approach to solving data-flow problems. Here we discuss another approach called *region-based analysis*. Recall that in the iterative-analysis approach, we create transfer functions for basic blocks, then find the fixed-point solution by repeated passes over the blocks. Instead of creating transfer functions just for individual blocks, a region-based analysis finds transfer functions that summarize the execution of progressively larger regions of the program. Ultimately, transfer functions for entire procedures are constructed and then applied, to get the desired data-flow values directly.

While a data-flow framework using an iterative algorithm is specified by a semilattice of data-flow values and a family of transfer functions closed under composition, region-based analysis requires more elements. A region-based framework includes both a semilattice of data-flow values and a semilattice of transfer functions that must possess a meet operator, a composition operator, and a closure operator. We shall see what all these elements entail in Section 9.7.4.

A region-based analysis is particularly useful for data-flow problems where paths that have cycles may change the data-flow values. The closure operator allows the effect of a loop to be summarized more effectively than does iterative analysis. The technique is also useful for interprocedural analysis, where transfer functions associated with a procedure call may be treated like the transfer functions associated with basic blocks.

For simplicity, we shall consider only forward data-flow problems in this section. We first illustrate how region-based analysis works by using the familiar example of reaching definitions. In Section 9.8 we show a more compelling use of this technique, when we study the analysis of induction variables.

### 9.7.1 Regions

In region-based analysis, a program is viewed as a hierarchy of *regions*, which are (roughly) portions of a flow graph that have only one point of entry. We should find this concept of viewing code as a hierarchy of regions intuitive, because a block-structured procedure is naturally organized as a hierarchy of regions. Each statement in a block-structured program is a region, as control flow can only enter at the beginning of a statement. Each level of statement nesting corresponds to a level in the region hierarchy.

Formally, a *region* of a flow graph is a collection of nodes *N* and edges *E* such that:

- 1. There is a header *h* in *N* that dominates all the nodes in *N*.
- 2. If some node *m* can reach a node *n* in *N* without going through *h*, then *m* is also in *N*.
