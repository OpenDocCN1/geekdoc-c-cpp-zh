so, the algorithm's total runtime is O(N³). If N is 30,000, that's 2.7 × 10¹³ steps. A computer running 1 million steps per second would need more than 10 months to build the arrays.

![](bbox=[0.133, 0.163, 0.453, 0.333])

**Figure 13-13:** To find the path from start_node to end_node with intermediate point via_node, you recursively find the paths from start_node to via_node and from via_node to end_node.

For really big networks, this algorithm is impractical, so you need to use one of the other shortest-path algorithms to find paths as needed. If you need to find many paths on a smaller network, perhaps one with only a few hundred nodes, you may be able to use this algorithm to precompute all the shortest paths and save some time.

# Summary

The algorithms described in this chapter are traversals of networks. The depth-first and breadth-first traversal algorithms visit a network's nodes in different orders. The connectivity, spanning tree, minimal spanning tree, and shortest-path algorithms also traverse the network in various ways. For example, the minimal spanning tree shortest-path algorithm traverses links in order of costs, and the label-setting shortest-path algorithm traverses links in order of the distances to their destination nodes.

The all-pairs shortest-path algorithm is a bit different. Instead of traversing the network, it builds a collection of N shortest-path trees, each of which you traverse the network.

The next chapter continues the discussion of networks. It explains more-advanced algorithms that let solve real-world problems such as task ordering, map coloring, and work assignment.