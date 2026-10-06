36 Limits of Computation

# 3.2 DECISION PROBLEMS

A computational problem is a mapping between sets of sequences. As a language is a set of strings (which are sequences), a computational problem can also be seen as a statement about strings. This connection is an important one, and is the basis of computation theory.

Most of the computer science algorithms in standard texts find something in a set of data (“find the shortest path from A to B in the given graph”) or manipulate a set of input (“sort this array into ascending order”) or “output the amounts for current paychecks for employees in this database”. A simplification—but one we will be able to show without really losing anything—is to restrict the problems considered to only yes/no answers.

# Definition 3.3

A decision problem is a computational problem with output from the set {yes, no}.

Thus, a decision problem can be restated as a set membership question if S is the set of yes instances, is this instance in S or not?

The input is encoded as a string; this can be done in various ways (it is easy to encode an integer or an English sentence; a little less easy to encode a graph—and how would you encode a map?). Encodings of graphs will be discussed later.

# Example

“Find the shortest path from A to B in graph G” becomes the decision problem: “Given a number k and a graph G with vertices A and B and the path A = v₁, v₂, ..., vᵢ = B, is this a valid path in G with length ≤ k?” Here, if we do not care about the actual vertices that make up the path, we can translate it to: “Given a number k and a graph G with vertices A, B, does G contain a path of length ≤ k from A to B?” This becomes the language problem (or decision problem):

Language problem L_{path\_of\_length\_k} = {k, G, A, B : k integer, G graph with vertices A and B, and G has a path from A to B of length ≤ k}