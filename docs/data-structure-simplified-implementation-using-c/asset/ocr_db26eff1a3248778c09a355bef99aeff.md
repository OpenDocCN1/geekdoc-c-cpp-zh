to refer the depth first search method explained and coded in tree traversal (section 7.4).

![](bbox=[0.18, 0.13, 0.85, 0.45])

Figure 13-18: Depth first traversal

In the breadth first search method, we start from the vertex V_i, once all the neighbors of the vertex V_i are visited then we visit the neighbour of neighbours, and will continue till each node is not visited. During visit of the node due care is to be exercised to avoid visiting any node twice. Breadth first search is similar to the BFS of binary tree. While traversing the vertex Vi, we identify all the neighbours of this vertex, once the neighbours are identified then they are inserted in a queue. Therefore, the edges inserted at the end are removed at end. To enable the level by level traversal, we can use two queue. Consider the graph of figure 13.18, the breadth first traversal can be pursued as follows:

+   i) Assume that we have visited first vertex and it is V1.

+   ii) Neighbours of the V1 are V2, V3, V4 therefore all of them need to be inserted into a queue.

+   iii) After insertion, one element from the queue is removed (de-queue), the item available at first position of the queue is removed first. In this case, the first vertex is V2 therefore it is removed and marked as visited.

+   iv) Neighbours of V2 are inserted at the rear side of the queue, in this case it is V5. Therefore, the resultant queue will be V3, V4, V5

+   v) This is followed by de-queue of the neighbors already inserted i.e. V3. Its neighbor is V6, therefore, it would be inserted in the queue. Consequently, the resultant queue would be V4,V5, V6.

+   vi) In the next step, we would de-queue from the queue, consequently, we would obtain V4. Neighbour of this node is V6 that is already visited therefore, no more node will be added. Consequently, the resultant queue would be V5, V6.