![](bbox=[0.21, 0.09, 0.83, 0.27])

# Figure 10.18 Huffman's algorithm after the fifth merge

Next, we must show that the two least frequent characters \(\alpha\) and \(\beta\) must be the two deepest nodes (although other nodes may be as deep). Again, this is easy to show by contradiction, since if either \(\alpha\) or \(\beta\) is not a deepest node, then there must be some \(\gamma\) that is (recall that the tree is full). If \(\alpha\) is less frequent than \(\gamma\), then we can improve the cost by swapping them in the tree.

We can then argue that the characters in any two nodes at the same depth can be swapped without affecting optimality. This shows that an optimal tree can always be found that contains the two least frequent symbols as siblings; thus, the first step is not a mistake.

The proof can be completed by using an induction argument. As trees are merged, we consider the new character set to be the characters in the roots. Thus, in our example, after four merges, we can view the character set as consisting of \(a\) and the metacharacters \(T3\) and \(T4\). This is probably the trickiest part of the proof; you are urged to fill in all of the details.

The reason that this is a greedy algorithm is that at each stage we perform a merge without regard to global considerations. We merely select the two smallest trees.

If we maintain the trees in a priority queue, ordered by weight, then the running time is \(O(C \log C)\), since there will be one buildHeap, \(2C - 2\) deleteMins, and \(C - 2\) inserts,

![](bbox=[0.21, 0.66, 0.83, 0.88])

# Figure 10.19 Huffman's algorithm after the final merge