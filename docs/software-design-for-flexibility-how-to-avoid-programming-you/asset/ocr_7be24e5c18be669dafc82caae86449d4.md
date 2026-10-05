If instead of choosing $R_2$ (remember to retract the support for this value!) she chooses to assert the $Z$ specification, this should determine $R_1$ and $R_2$; but the network will not find the value of $R_2$! Why? Explain this problem.

+   d. If we now tell $R_2$ that it is somewhere in the range of 1000 ohms to 500000 ohms, the propagator network will converge to give a useful answer for the real range of $R_2$. Why? Explain this!

# Exercise 7.3: Local consistency—a project

Propagation is a way of attacking local consistency problems. For example, the Waltz algorithm [125] is a propagation method for interpreting line drawings of solid polyhedra. Map coloring and similar problems can be successfully attacked using propagation.

The essential idea is that there is a graph with nodes that can be assigned one of a set of discrete labels, and that the nodes are interconnected by constraints that limit which labels are allowed based on the labels in neighboring nodes. For example, in the Waltz algorithm a line may have one of several labels. Each line connects two vertices. A vertex constrains the lines terminate on it to be consistent with one of a set of possible geometric interpretations of the vertex. The interpretation of a line must be the same at both ends of the line.

+   a. For these experiments you will need an “arithmetic” of discrete sets. You will need unions, intersections, and the complement of one in another. Build such an arithmetic.

+   b. The set of possibilities for a node is partial information about the actual status of the node: the smaller the set of possibilities the more information we have about the node. If we represent the knowledge about the status of a node as a propagator cell, the merger of two sets is their intersection. This is consistent with the intersection of intervals for ranges of real values. Make intersection of discrete sets a handler for generic merge.