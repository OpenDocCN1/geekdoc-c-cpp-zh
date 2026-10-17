# ### 9.4.3. Deletion

You may recollect that the deletion of node in a singly linked list entailed in finding the predecessor of the discarded node and the deletion was done. The search was done by chaining through successive nodes. The search was mandatory and such a search can be quite cumbersome and it could become painstaking if the list was long and number of nodes to be deleted was more. In a doubly linked list no such search is required. Given the address of the node which is to be deleted its successor and predecessor nodes can be known immediately. Similar to the insertion operation the deletion operation also can be performed in the following locations:

+   - If list is empty;
+   - At the beginning of the list;
+   - In between the nodes.

# ## 9.5. CIRCULAR LINKED LISTS

The early parts of the session were exclusively concerned with the linked linear lists and its different forms performing variant functions. All the linked lists that you have dealt so far had one thing in common. They were terminated with a null. A slight modulation in the structure of the linked list can now be performed which results in improving the processing the list. The circular linked lists believes that there is no need for the existence of the null and that the integrity of the linked list can be maintained and revamped without the null. This is accomplished by replacing the null in last node with the address of the first node. With the incorporation of the circular linked list a few rules, which held water earlier, are bent. The first of them of being that there is no first node once a circular list is created. The node where the head pointer is made to point in a circular list becomes the starting point for traversing the list. Thus, any node of your choice can be accessed directly for the first time. To examine the effectiveness of the circular list, it’s coexistence in both the forms of the linear linked lists is evaluated. Thus, there can exist:

+   1. **Circular Singly Linked List:** In circular singly linked lists, the null pointer in the last node of a singly linked list is replaced with the address of the first node of the list. By achieving the above feat a circular singly linked list is created and the accessibility of a node is increased. Hence all the nodes can be accessed by merely scanning through the list.