Deletion Operations: Deletion in a linked list can be done by locating the node to be deleted and adjusting the pointers to bypass the deleted node.

Deletion by key: Here, we search for a node with a specific key, then update the pointers to remove it from the list.

```
void deleteNodeByKey(Node** head, int key) { *temp = *head, *prev = NULL; (temp != NULL && temp->data != key) { temp = temp->next; (temp != NULL && temp->data != key) { temp = temp->next; (temp == NULL) // Key not found = temp->next; } }
```

Traversal: Traversing a linked list involves sequentially accessing each node until the end is reached. This is often implemented using a loop to visit each node.

```
void printLinkedList(Node* node) { (node != NULL) { node->data); = node->next; }
```

By understanding and implementing these operations, you gain the flexibility to manage data structures dynamically, tailoring them to the specific needs of your applications. Linked lists serve as the foundation for more complex structures like stacks, queues, and even graph representations, showcasing their versatility and importance in computer science.

# 3.2