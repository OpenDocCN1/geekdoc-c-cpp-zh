reach any of the nodes that precede the node to which A is pointing. This disadvantage can be overcome by making a small change. This change is without any additional data structure. The link field of the last node is set to `null` in a linear list to mark the end of the list. This link field of the last node can be set to point to the first node rather than `null`. Such a linked list is called a circular linked list (Fig. 6.27).

![](bbox=[0.253, 0.233, 0.856, 0.303])

Fig. 6.27 Circular linked list

From any node in such a list, it is possible to reach any other node in the list. A circular list could be singly circular or doubly circular list and with or without a header node. Circular lists have many applications. We shall study those in further topics. Linear lists are also called non-circular or grounded lists. The last node's link field of a linear list is set to `null`. It is pictorially denoted using the 'ground' symbol used in electronic circuits. Let us discuss the DLL and its operations.

# 6.7 DOUBLY LINKED LIST

In SLL, each node provides information about where the next node is. It has no knowledge about where the previous node is. For example, if we are at the i<sup>th</sup> node in the list currently, then to access the (i – 1)<sup>th</sup> node or (i – 2)<sup>th</sup> node, we have to traverse the list right from the first node. In addition, it is not possible to delete the i<sup>th</sup> node given only a pointer to the i<sup>th</sup> node. It is also not possible to insert a node before the i<sup>th</sup> node given only a pointer to the i<sup>th</sup> node (there are other ways that are without link manipulations such as using data exchange). For handling such difficulties, we can use DLLs where each node contains two links, one to its predecessor and other to its successor (Fig. 6.28).

![](bbox=[0.253, 0.743, 0.856, 0.803])

Fig. 6.28 Doubly linked list of four nodes

Each node of a DLL has three fields in general but must have at least two link fields (Fig. 6.29).