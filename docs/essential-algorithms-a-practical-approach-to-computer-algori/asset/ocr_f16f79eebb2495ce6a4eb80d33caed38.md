# Label-Correcting Shortest Paths

The time-consuming step in label-setting shortest-path algorithm is finding the next link to add to the shortest-path tree. To add a new link to the tree, the algorithm must search through the candidate links to find the one that reaches a new node with the least cost.

An alternative strategy is to just add any of the candidate links to the shortest-path tree and its destination node with the root as usual.

Later, when the algorithm considers links in that is already in the shortest-path tree, it may find a better path to a node. In that case, the algorithm updates the node's distance, adds its links back into the candidate list (if they are not already in the list), and continues.

In the label-setting algorithm, a node's distance is set only once and never changes. In the label-correcting algorithm, a node's distance is set once but later may be corrected many times.

The following describes the algorithm at a high level:

+   1. Setting the node's distance to 0, and mark it as part of the tree.
2. Add the setting node's links to a candidate list of links.
3. While the candidate list is not empty:
a. Consider the first link in the candidate list.
b. Calculate the distance to the link's destination node: <distance> = <link cost>
c. If the new distance is better than the destination node's current distance:
ni. Update the destination node's distance.
ii. Add all the destination node's links to the candidate list.

This algorithm may seem more complicated, but the code is actually shorter, because you don't need to search the candidate list for the best link.

Because this algorithm may change the link leading to a node several times, you cannot simply mark a link as used by the tree and leave it at that. If you need to change the link that leads to a node, you need to find the old link and unmark it.

An easier approach is to give the Node class a FromLink property. When you change the link leading to the node, you can update this property.

If you still want to mark the links used by the shortest-path tree, first build the tree. Then loop over the nodes and the links stored in their FromLink properties.

Figure 3-11 shows the shortest-path tree for a network found using the label-correcting method. Again, in this network the links' costs are their lengths in pixels. Each node is labeled with the number of times its distance (and FromLink