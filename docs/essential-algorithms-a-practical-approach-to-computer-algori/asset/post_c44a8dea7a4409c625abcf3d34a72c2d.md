
describe a simple high-level algorithm for finding a path from node A to node B in a network:

- Find a spanning tree rooted at node A.
- Follow the reversed links in the spanning tree from node B to node A.
- Reverse the order in which the links were followed.

The algorithm builds the spanning tree rooted at node A. Then it starts at node B. For each node in the path, it finds the link in the spanning tree that leads to node A. It records that link and moves to the next node in the path.

Unfortunately, finding the link that leads to a particular node in the spanning tree is difficult. Using the spanning tree algorithms so far, you would need to loop through every link to determine whether it was part of the spanning tree and whether it ended at the current node.

You can solve this problem by making a small change to the spanning tree algorithm. First, add a new FromNode property to the Node class. Then, when the spanning tree marks a node as being in the tree, set that node's FromNode property to the link link was used to connect the new node to the tree.

Now, to find the path from node B to node A in step 2, you can simply follow the nodes' FromNode properties.

## Label-Setting Shortest Paths

The algorithm described in the preceding section finds a path from a start node to a destination node, it's not necessarily a very good path. The path is taken from a spanning tree, and there's no guarantee that it is very efficient. Figure 13-7 shows how to find a shorter path such as M → L → G → H → I → N → S.

A more useful algorithm would find the shortest path between two nodes. Shortest-path algorithms are divided into two categories: label setting and label correcting. The next section describes a label-correcting algorithm. This section describes a label-setting algorithm.

This label-setting algorithm begins at a starting node and creates a spanning tree in a manner that is somewhat similar to how the minimal spanning tree described earlier. At each step, that algorithm selects the least-cost link that connects a new node to the spanning tree. In contrast, the shortest-path algorithm selects a link that adds to a tree that is the least distance from the starting node.

To determine which node is the least distance from the starting node, the algorithm labels each node with its distance from the starting node. When it considers a link, it adds the distance to the link's source node to link's cost, and that determines the current distance to the link's destination node.

![](img/fefa42765c0b410af6705110aea7c0cb_364_0.png)

**Figure 13-7:** A path that follows a spanning tree from one node to another may be inefficient.

When the algorithm has added every node to the spanning tree, it is finished. The paths through the tree show the shortest paths from the starting node to every other node in the network, so the tree is called a *shortest-path tree*. The following describes the algorithm at a high level:

1. Set the starting node's distance to 0, and mark it as part of the tree.
2. Add the starting node's links to a candidate list of links that could be used to extend the tree.
3. While the candidate list is not empty, loop through the list examining the links.
   a. If a link leads to a node that is already in the tree, remove the link from the candidate list.
   b. Suppose link L leads from node $N_i$ to tree node $N_j$, not yet in the tree. If $D_i$ is the distance to node $N_i$ in the tree and $C_{ij}$ is the cost of the link, then you could reach node $N_j$ with distance $D_i + C_{ij}$, by first going to node $N_i$ and following the link. Let $D_j = D_i + C_{ij}$ be the possible distance for node $N_j$ that uses this link. As you loop over the links in the candidate list, keep track of the link and node that give the smallest distance. Let $L_{best}$ and $N_{best}$ be the link and node that give the smallest distance $D_{best}$.
   c. Set the distance for $N_{best}$ to $D_{best}$ and mark $N_{best}$ as part of the tree.
   d. For all links L leaving $N_{best}$ if L leads to a node that is not yet in the tree, add L to the candidate list.

For example, consider the network shown on the left in Figure 13-8. Suppose the bold links and nodes are part of a growing shortest-path tree. The tree’s nodes are labeled with their distance from the root, which is 0.

![](img/fefa42765c0b410af6705110aea7c0cb_365_0.png)

**Figure 13-8:** At each step, add the shortest-path tree that gives the smallest distance from the root to a node that is not in the tree.

To add the next link to the tree, examine the links that lead from the tree to a node that is not in the tree, and calculate the distance to these nodes. For example has three possible links: the first leads from the node labeled 19 to F. The distance from the root to the node labeled 19 is 19, and this link has cost 11, the total distance to F via this is $19 + 11 = 30$. The second link leads from the node labeled 15 to F. The distance from the root to the node labeled 15 is 15, and this link has cost 11, so the total distance to F via this is $15 + 11 = 26$. The third link leads from the node labeled 10 to G. The link has cost 12, the total distance via link is $10 + 12 = 22$. This is one of the three distances calculated, so this is the link that should be added to the tree. The result is shown on the right in Figure 13-8.

Figure 13-9 shows a complete shortest-path tree by this algorithm. In this network, the links’ costs are their lengths. Each node is labeled with the order in which it was added to the tree. Notice how the nodes’ labels increase as the distance from the root increases. This is similar to breadth-first traversal. The difference is that the breadth-first traversal added nodes in order of the number of links between the root and the nodes, but this algorithm adds nodes in order of the distance along the links between the root and nodes.

![](img/fefa42765c0b410af6705110aea7c0cb_366_0.png)

**Figure 13-9:** A shortest-path tree gives the shortest paths from the root node to any node in the network.

Having built a shortest-path tree, you can follow the nodes' FromNode values to find a backwards path from a destination node to the start node, as described in the preceding section.

Figure 13-10 shows the shortest path from node M to S in the original network. This looks more reasonable than the path shown in Figure 13-7, which uses a spanning tree.

![](img/fefa42765c0b410af6705110aea7c0cb_366_1.png)

**Figure 13-10:** A path through a shortest-path tree gives the shortest path from the root node to a specific node in the network.

## Label-Correcting Shortest Paths

The time-consuming step in label-setting shortest-path algorithm is finding the next link to add to the shortest-path tree. To add a new link to the tree, the algorithm must search through the candidate links to find the one that reaches a new node with the least cost.

An alternative strategy is to just add any of the candidate links to the shortest-path tree and its destination node with the root as usual.

Later, when the algorithm considers links that are already in the shortest-path tree, it may find a better path to a node. In that case, the algorithm updates the node's distance, adds its links back into the candidate list (if they are not already in the list), and continues.

In the label-setting algorithm, a node's distance is set only once and never changes. In the label-correcting algorithm, a node's distance is set once but later may be corrected many times.

The following describes the algorithm at a high level:

1. Set the node's distance to 0, and mark it as part of the tree.
2. Add the node's links to a candidate list of links.
3. While the candidate list is not empty:
   a. Consider the first link in the candidate list.
   b. Calculate the distance to the link's destination node: <distance> = <link cost>
   c. If the new distance is better than the destination node's current distance:
      i. Update the destination node's distance.
      ii. Add all the destination node's links to the candidate list.

This algorithm may seem more complicated, but the code is actually shorter, because you don't need to search the candidate list for the best link.

Because this algorithm may change the link leading to a node several times, you cannot simply mark a link as used by the tree and leave it at that. If you need to change the link that leads to a node, you need to find the old link and unmark it.

An easier approach is to give the Node class a FromLink property. When you change the link leading to the node, you can update this property.

If you still want to mark the links used by the shortest-path tree, first build the tree. Then loop over the nodes and the links stored in their FromLink properties.
