+   - Allocate memory for the new node and set its data field if it is known at the time of allocation:
+     ```c
+     struct node *p;
+     p = malloc(sizeof(struct node));
+     p->data = 111;
+     ```

+   - Set the `.next` pointer of the new node to point to the original first node. This latter node is accessed by the head pointer:
+     ```c
+     p->next = head;
+     ```
+     *This assignment has to be made ...*

+   - Reassign the head pointer to point to the new node:
+     ```c
+     head = p;
+     ```
+     *... before this one.*

This is a simple and fast technique compared to the one used for insertion of an array element (10.5.1). Simply create memory for the new node, assign values to one or more data fields and realign two pointers. Nothing can be simpler than that!

![](bbox=[0.174, 0.383, 0.825, 0.569])

# 16.11.2 Adding a Node at End

For adding a node at the end of the list, first traverse the entire list to reach its end. The process may be iterative or recursive, and requires the following steps to be taken:

+   - Allocate memory in the usual manner for the new node and assign its data field if necessary. Also, set its `.next` pointer to NULL.
+   - For an iterative traversal of the list to reach its end, use a copy of the head pointer as a key variable:
+     ```c
+     current = head;
+     while (current->next != NULL)
+         current = current->next;
+     ```
+     *Last node has `.next` set to NULL*
+   - Set the `.next` pointer of the original last node (which was previously set to NULL) to point to the new node.

The assignment, `current = current->next;`, needs to be examined closely since it is used in many list operations. This statement changes the address of the current node in every loop iteration. It thus lets every node in the list to be accessed. However, since the traversal is sequential, it is slow compared to random access of an array element.