# 532 Appendix B Solutions to Exercises

![](bbox=[0.133, 0.086, 0.703, 0.323])

**Figure B-21:** Because the graph of logarithm of nodes visited versus number of weights is a line, the difference is exponential in the number of nodes.

+   11. The two groups are [5, 6, 7, 7, 7] and [5, 6, 7, 7, 9]. Their total weights are 32 and 34, so the difference is 2.

+   12. The two groups are [7, 9, 7, 5] and [6, 7, 7, 7, 6]. Their total weights are both 33, so the difference is 0.

+   13. Example program PartitionProblem does this.

# Chapter 13: Basic Network Algorithms

+   1. Example program NetworkMaker does this. Select the Add Node tool and click on the drawing to create new nodes. When you select either of the add links, use the left mouse button to select the start node and use the right mouse button to select the destination node.

+   2. Example program NetworkMaker does this.

+   3. Example program NetworkMaker does this.

+   4. That algorithm does not work for directed networks because it assumes if there is a path from node A to node B, there is a path from node B to node A. For example, suppose a network has three nodes in a row A → B → C. If the algorithm starts at node A, it reaches all nodes, but if it starts at node B, it only finds nodes B and C. It would incorrectly conclude that the network has two connected components [B, C] and [A].

+   5. Example program NetworkMaker does this.

+   6. If the network has N nodes, any spanning tree contains exactly N – 1 links. If the links have the same cost C, every spanning tree has a total cost of C × (N – 1).

+   7. Example program NetworkMaker does this.