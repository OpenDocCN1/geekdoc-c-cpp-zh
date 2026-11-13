![](bbox=[0.203, 0.082, 0.918, 0.243])

![](bbox=[0.203, 0.282, 0.816, 0.423])

The special case of adding at the end (i.e., making the new item the last item) can be constant-time, as long as we maintain a link to the last node. Thus, a typical linked list keeps links to both ends of the list. Removing the last item is trickier, because we have to find the next-to-last item, change its next link to nullptr, and then update the link that maintains the last node. In the classic linked list, where each node stores a link to its next node, having a link to the last node provides no information about the next-to-last node.

The obvious idea of maintaining a third link to the next-to-last node doesn't work, because it too would need to be updated during a removal. Instead, we have every node maintain a link to its previous node in the list. This is shown in Figure 3.4 and is known as a doubly linked list.

# ## 3.3 vector and list in the STL

The C++ language includes, in its library, an implementation of common data structures. This part of the language is popularly known as the Standard Template Library (STL). The List ADT is one of the data structures implemented in the STL. We will see some others in Chapters 4 and 5. In general, these data structures are called collections or containers.

There are two popular implementations of the List ADT. The vector provides a growable array implementation of the List ADT. The advantage of using the vector is that it is indexable in constant time. The disadvantage is that insertion of new items and removal of existing items is expensive, unless the changes are made at the end of the vector. The list provides a doubly linked list implementation of the List ADT. The advantage of using the