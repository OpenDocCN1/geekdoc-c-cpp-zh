**Data node** The list contains data nodes that store the data members and link(s) to its predecessor (and/or successor).

**Head pointer** The variable (or handle), which represents the list, is simply a pointer to the node at the head of the list. A linked list must always have at least one pointer pointing to the first node (head) of the list. This pointer is necessary because it is the only way to access the further links in the list. This pointer is often called *head pointer*, because a linked list may contain a dummy node attached at the start position called the *header node*.

**Tail pointer** Similar to the head pointer that points to the first node of a linked list, we may have a pointer pointing to the last node of a linked list called the *tail pointer*.

# ## 6.2.3 Primitive Operations

The following are basic operations associated with the linked list as a data structure:

+   1. Creating an empty list
+   2. Inserting a node
+   3. Deleting a node
+   4. Traversing the list

Some more operations, which are based on the basic operations, are as follows:

+   5. Searching a node
+   6. Updating a node
+   7. Printing the node or list
+   8. Counting the length of the list
+   9. Reversing the list
+   10. Sorting the list using pointer manipulation
+   11. Concatenating two lists
+   12. Merging two sorted lists into a third sorted list

In addition, operations such as merging the second sorted list into the first sorted list and many more are possible by the use of these operations.

# ## 6.3 REALIZATION OF LINKED LISTS

In a linked organization, the data elements are not necessarily placed in continuous locations. The relationship between data elements is by means of a link. Along with each data element, the address of the next element is stored. Thus, the associated link with each data element to its successor is often referred to as a *pointer*. In general, a *node* is a collection of data and link(s). *Data* is a collection of one or more items. Each item in a node is called a *field*. A field contains either a data item or a link. Every node must contain at least one link field.