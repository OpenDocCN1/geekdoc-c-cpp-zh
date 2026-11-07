+   f. To insert a new item in a linked list, create a node, store the new item in the node, and insert the node in the linked list. (3)
+   
+    g. To build a linked list forward, the new node is inserted at the end of the list. (4)
+   
+    h. A single linked list can be traversed in either direction. (2, 4, 5)
+   
+    i. In a linked list, nodes are always inserted either at the beginning or at the end because a linked list is not a random-access data structure. (4, 5, 8, 9)
+   
+    j. The head pointer of a linked list should not be used to traverse the list. (2, 4, 7)
+   
+    k. The two most common operations on iterators are ++ and * (the dereferencing operator). (6)
+   
+    l. The function `initializeList` of the class `linkedListType` initializes the list by only setting the pointers `first` and `last` to `nullptr`. (7)
+   
+    m. The function `search` of the class `unorderedLinkedList` searches the linked list sequentially, while the function `search` of the class `orderedLinkedList` searches the list using a binary search algorithm because the data in an `orderedLinkedList` object is sorted. (8, 9)
+   
+    n. A doubly linked list can be traversed in either direction. (10)

+   2. Describe the two typical components of a single linked list node. (1)

+   3. What is stored in the link field of the last node of a nonempty single linked list? (2)

+   4. Suppose that `first` is a pointer to a linked list. What is stored in `first`? (2)

+   5. Suppose that the fourth node of a linked list is to be deleted, and `p` points to the fourth node? Why do you need a pointer to the third node of the linked list? (3)

Consider the linked list and the variable declaration shown in Figure 16-50, where `nodeType` is a `struct` with two components: `info` of type `int` and `link` of type `nodeType`. Use this list to answer Exercises 6 through 14.

![](bbox=[0.182, 0.8, 0.906, 0.935])

FIGURE 16-50  Linked list for Exercises 6–14.