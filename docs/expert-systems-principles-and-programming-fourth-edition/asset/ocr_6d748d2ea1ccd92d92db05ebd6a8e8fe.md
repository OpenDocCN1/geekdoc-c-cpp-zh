# 3.2 TREES, LATTICES, AND GRAPHS

A tree is a hierarchical data structure consisting of nodes, which store information or knowledge and branches, which connect the nodes. Branches are sometimes called links or edges and nodes are sometimes called vertices. Figure 3.1 shows a general binary tree which has zero, one, or two branches per node. In an oriented tree the root node is the highest node in the hierarchy and the leaves are the lowest. A tree can be considered a special type of semantic net in which every node except the root has exactly one parent and zero or more child nodes. For the usual type of binary tree there is a maximum of two children per node, and the left and right child nodes are distinguished.

# Figure 3.1 Binary Tree

![](bbox=[0.112, 0.338, 0.92, 0.58])

If a node has more than one parent, it is in a network. In Figure 3.1, notice that there is only one sequence of edges or path from the root to any node since it is not possible to move against an arrow. In oriented trees the arrows all point downward.

Trees are a special case of a general mathematical structure called a graph. The terms network or simply net are often used synonymously with graph when describing a particular example such as an ethernet network. A graph can have zero or more links between nodes and no distinction between parents and children. A simple example of a graph is a map, where the cities are the nodes and the links are the roads. The links may have arrows or directions associated with them and a weight to characterize some aspect of the link. An analogy is one-way streets with limits on how much weight trucks can carry. The weights in a graph can be any type of information. If the graph represents an airline route, the weights can be miles between cities, cost of flying, fuel consumption, and so forth.

A supervised artificial neural network is another example of a graph with cycles since during training there is feedback of information from one layer of the