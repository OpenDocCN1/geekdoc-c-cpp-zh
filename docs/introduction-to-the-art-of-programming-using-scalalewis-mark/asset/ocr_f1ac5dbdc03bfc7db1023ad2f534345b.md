# List of Figures

31.1 This figure shows an example set of points with a very non-uniform spatial distribution. A regular grid is laid over this to make clear how the point density in the grid cells will vary dramatically. The grid size shown here works well for many of the low-density regions where there are only a handful of particles per cell. A grid that only had a few particles per cell in the high-density regions would be a very fine grid with an extremely large fraction of the cells being empty in the low-density areas.

31.2 This is a quadtree with a number of non-uniformly distributed points to illustrate how the space is partitioned. For this example, each node is only allowed to hold a single point. The key advantage of the tree-based approach is that the resolution does not have to be uniform. Higher-density regions can divide the space much more finely.

31.3 This is a kD-tree with a number of non-uniformly distributed points to illustrate how the space is partitioned. For this example, each node can hold up to three points. While this example only uses two dimensions, it is simple to scale the kD-tree up higher without adding overhead.

32.1 This figure shows an example of a binary heap. The numbers are priorities with higher values being higher priority. Note that there is no problem with duplicate priorities, unlike keys in a BST.

32.2 This figure shows the same heap as in figure 32.1 with subscripts that number the nodes in breadth-first order. Below that is an array with the elements at those locations.

32.3 Adding a new element with a priority of 9 to the heap shown in figure 32.1 goes through the following steps. A bubble is added at the next location in a complete tree. It moves up until it reaches a point where the new value can be added without breaking the heap-order.

32.4 Calling dequeue on the heap at the end of figure 32.3 forces the tree to go through the following steps. The last element is moved to a temporary variable and a stone is placed at the top of the heap. This stone sinks down until it reaches a point where the temporary can stop without breaking heap-order. The stone always sinks in the direction of the higher-priority child.

32.5 This shows a pictorial representation of the alternate data structure that can be used as an efficient priority queue for collision handling. The top array keeps the heads of lists for different time brackets during the time step. The left array is the heads of lists for different particles. All lists are doubly linked so that nodes can be removed without finding the one before it.

33.1 The binary file holding the linked list has the following format. The beginning of the file is a header with four values written as Longs. They are the position of the head node, the position of the tail node, the number of nodes, and the position of the first free node.

33.2 The nodes of a B-tree can store a certain number of records. The number of records is selected to match an optimal size for disk reads and writes. Non-leaf nodes have references to children at the beginning, end, and between each record. The records in a node are sorted by a key. In addition, the nodes in children have to have key values that fall between the keys of the records they are between, or just below and above for the beginning and end children. B-trees are always balanced and require few disk accesses to find a record, but they do potentially waste some space.