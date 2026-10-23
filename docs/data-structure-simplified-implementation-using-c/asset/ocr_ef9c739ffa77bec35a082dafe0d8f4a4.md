```
{
    cout<<current->data<<" <-> ";
    current=current->prev;
}
cout<<endl;
}
```

# 4.5 INSERTING ITEM (NODE) IN A DOUBLY LINK LIST

In a doubly link list, a new node can be inserted at any position including first, middle or at last position. In a doubly link list insertion of the node is less cumbersome relative to the singly link list. Complexity is reduced due to the availability of two pointers that exist in the doubly link list. During insertion of a node in a doubly link list, following sequence of steps need to be followed:

+   - Accept the position where new node is to be inserted.
+   - Intending position where node is to be inserted should be less than or equal to length of the doubly link list, if it is more than total number of nodes, in that case node cannot be inserted.
+   - If the above condition is fulfilled, then traverse upto the node that is just before which the node is to be inserted. Assume that this node is termed as previous node.
+   - Find out the next pointer of the current node.
+   - Connect the new node with the forward node and the node lies before this current node i.e. previous node.
+   - If the node is to be inserted at the first position in that case the pointer of the first node should be changed to this new node.
+   - Similarly, if the node to be inserted is the last node, change the pointer of the last node to this new node.

All the above cases have been discussed in forthcoming sub-sections.

# A. Insertion at the beginning

In a doubly link list, node can be inserted at the beginning of a link list but in that case the first pointer will be shifted to this new node that is attached at the first position. Complete process has been defined as follows:

+   - Create the new node.
+   - Connect its next pointer to the already existing first pointer.
+   - Change the exisiting first node’s pointer to the pointer of the node that has been just inserted.