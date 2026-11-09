# ### 9.6.4 Hierarchical or Pyramidal Algorithms

A commonly used hierarchical algorithm used in chemoinformatics and elsewhere is Wards algorithm. A fast implementation of this algorithm uses RXN. RXN can also be employed similarly with two other common hierarchical algorithms, complete link, and group average. Decision ties that lead to clustering ambiguity reside directly within RXN. The core operation of RXN is to form a nearest neighbor (NN) chain until a RXN (each is the NN of the other) is found. Two questions arise in its implementation: What if there is more than one NN? And what if in turn there is more than one RXN? An NN chain assumes that each NN is unique. Given ties in proximity however, for any given data item there may be more than one NN. If the chain is altered arbitrarily due to ties. this situation gives rise to the second question. namely, the resulting RXN may also differ. RXNs may represent either data items or merged groups in the agglomerative process via the merging criterion in the implementation of this class of hierarchical algorithms. As represented in the dendrogram. arbitrary decisions are embedded where ever they occur within the tree. The amount of ambiguity is related to the similarity coefficient and the merging criterion. In complete link the RXNs are always the coefficient values and the ambiguity inherent in any dendrogram derived there from is directly related to ties in proximity of the coefficient values. Group average and Wards algorithms however contain derived merging criteria that are less likely to contain ambiguity. in large measure based on the complexity of the merging criterion. Hierarchical algorithms can in general be transformed into pyramidal clustering [2. 7. 8. 107] with the use of these forms of decision ties.

# ### 9.7 Glossary

+   * decision tie: a numerical or categorical tie leading to an arbitrary decision within an algorithm
+   * discrete: categorical, binary, or count data
+   * tie in proximity: identical distance or similarity score

# ### 9.8 Exercises

+   1. Generate four example distributions of the Tversky similarity measure, given the same five-bit fingerprint used to show the similarity values of the Tanimoto measure in Figure 2.5, and the similarity values of the