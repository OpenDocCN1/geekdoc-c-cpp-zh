![](bbox=[0.05, 0.08, 0.8, 0.22])

Figure 11.8 Change in heavy/light status after a merge

# Proof

Let H1 and H2 be the two heaps, with N1 and N2 nodes, respectively. Suppose the right path of H1 has l1 light nodes and h1 heavy nodes, for a total of l1 + h1 nodes. Likewise, H2 has l2 light and h2 heavy nodes on its right path, for a total of l2 + h2 nodes.

If we adopt the convention that the cost of merging two skew heaps is the total number of nodes on their right paths, then the actual time to perform the merge is l1 + l2 + h1 + h2. Now the only nodes whose heavy/light status can change are nodes that are initially on the right path (and wind up on the left path), since no other nodes have their subtrees altered. This is shown by the example in Figure 11.8.

If a heavy node is initially on the right path, then after the merge it must become a light node. The other nodes that were on the right path were light and may or may not become heavy, but since we are proving an upper bound, we will have to assume the worst, which is that they become heavy and increase the potential. Then the net change in the number of heavy nodes is at most l1 + l2 - h1 - h2. Adding the actual time and the potential change (Equation (11.2)) gives an amortized bound of 2(l1 + h2).

Now we must show that l1 + l2 = O(log N). Since l1 and l2 are the number of light nodes on the original right paths, and the right subtree of a light node is less than half the size of the tree rooted at the light node, it follows directly that the number of light nodes on the right path is at most log N1 + log N2, which is O(log N).

The proof is completed by noting that the initial potential is 0 and that the potential is always nonnegative. It is important to verify this, since otherwise the amortized time does not bound the actual time and is meaningless.

Since the insert and deleteMin operations are basically just merges, they also have O(log N) amortized bounds.

# 11.4 Fibonacci Heaps

In Section 9.3.2, we showed how to use priority queues to improve on the naive O(|V|^2) running time of Dijkstra's shortest-path algorithm. The important observation was that the running time was dominated by |E| decreaseKey operations and |V| insert and deleteMin operations. These operations take place on a set of size at most |V|. By using a binary heap, all these operations take O(log |V|) time, so the resulting bound for Dijkstra's algorithm can be reduced to O(|E| log |V|).