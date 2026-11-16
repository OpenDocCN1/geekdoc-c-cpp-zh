![](bbox=[0.15, 0.1, 0.75, 0.25])

Figure 11.14 LEFT: A range camera has observed a scene and segmented it into segments that satisfy the same equation, however, an error has occurred. RIGHT: The nodes of the resulting association graph.

# 11.7.1 Association Graphs

Association graphs are one technique for labeling that is particularly easy to visualize.

An association graph embodies a methodology that is less restrictive than isomorphism, and that may converge more rapidly. It will converge to a solution that is consistent but not necessarily optimal (depending, of course, on the criteria for optimality used in any particular application).

The method matches a set of nodes from the model to a set of nodes extracted from the image.

Definition: An association graph is denoted G = < V, P, R >, where V represents a set of nodes, P represents a set of unary predicates on nodes, and R represents binary relations between nodes.

A predicate is a statement that takes on only the values TRUE or FALSE. For example let x denote a region in a range image. Then CYLINDRICAL(x) is a predicate that is true or false depending on whether all the pixels in x lie on the same cylindrical surface.

A binary relation describes a property possessed by a pair of nodes, such as ABOVE(a, b). Given two graphs: G1 = < V1, P1, R1 > and G2 = < V2, P2, R2 >, we construct the association graph G = < VA, R > by:

+   - for each v1 in V1 and v2 in V2, if v1 and v2 have the same properties, construct a node of G denoted (v1, v2).
+   - If lambda in R and lambda(v1, v1') => lambda(v2, v2'), add an edge to RA that connects (v1, v1') to (v2, v2'). Here, the symbol => means "is consistent with."

The best match of G1 to G2 is determined by finding the largest clique of G. Figure 11.14 RIGHT illustrates the nodes of an association graph.

Like every other technique in Computer Vision, we need to ask, “How good is this method?” Some problems arise when attempting to answer that question.

Problem 1: Is the largest clique the best match?

The largest clique is the largest set of consistent matches. Is this really the best match?