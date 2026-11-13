independent of the size of the list.

+   v) The joining of two linked lists can be done by assigning pointer of the second linked list in the last node of the first linked list.

Splitting can be done by assigning a null address in the node from where we want to split one linked list into two parts.

# Types of linked list

There are different types of linked list. We can put linked lists into the following four types:

+   i) Singly linked list
+    ii) Circular Linked list
+    iii) Doubly Linked list
+    iv) Circular Doubly linked list

# Singly linked list

An element in a linked list is specially termed as a node. In a singly linked list, each node consists of two fields:

+   i) DATA field that contains the actual information of the element.
+    ii) LINK field, contains the address of the next node in the list.

A "DATA" field to store whatever element type list holds for the user, and a "LINK" field, which is a pointer, used to link one node to the next node. Each node is allocated in the heap with a call to malloc() function. The node memory becomes free when it is explicitly de-allocated with a call to free() function. The front of the list is a pointer to the first node. Here is what a list containing the numbers 1, 2, and 3 might look like.

![](bbox=[0.18, 0.53, 0.76, 0.64])

Figure 5.1: Linked list representation

# Operations on Singly linked list

Operations supported by a singly linked list are as follows:

Table 5.2: Various Operation on Linked list

| Operation | Description |
| :--- | :--- |
| Createlist | This operation creates a linked list. |
| Traverse | This operation traverse/visit all the elements of the linked list exactly once |
| Insertion | This operation inserts an element to the linked list |
| Deletion | This operation removes an element from the linked list |
| Searching | This operation performs linear searching for a key value in the linked list |
| Reverse | This operation performs the reverse of the linked list |
| Merging | This operation performs merging of two linked lists in a single linked list |