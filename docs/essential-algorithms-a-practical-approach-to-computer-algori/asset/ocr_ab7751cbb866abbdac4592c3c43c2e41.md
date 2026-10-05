value) was corrected. The root node is labeled 0 because its value was set initially and never changed.

![](bbox=[0.191, 0.15, 0.606, 0.436])

**Figure 13-11:** In a label-correcting algorithm, some nodes' distances may be corrected several times.

In a large and more complicated network, it is possible that a node's distance might be corrected many times before the shortest-path tree is complete.

# All-Pairs Shortest Paths

The shortest-path algorithms described so far find shortest-path trees from a starting node to every other node in the network. Another type of shortest-path algorithm allows you to find the shortest path between every pair of nodes in the network.

The Floyd-Warshall algorithm begins with a two-dimensional array named Distance, where Distance[start_node, end_node] is the shortest distance between nodes `start_node` and `end_node`.

To build the array, initialize it by setting the diagonal entries, which represent the distance from a node to itself, to 0. Set the entries that represent direct links between two nodes to the cost of the links. Set the array's other values to infinity.