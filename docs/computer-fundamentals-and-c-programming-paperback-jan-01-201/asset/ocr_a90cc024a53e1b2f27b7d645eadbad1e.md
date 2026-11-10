# ### 16.14.4 The insert_after Function

```
```c
void insert_after(struct node *head, short val1, short val2)
{
    struct node *q, *found_node;
    found_node = find_node(head, val1);

    if (found_node == NULL)
        printf("Search value not found\n");
    else {
        q = malloc(sizeof(struct node));
        q->data = val2;
        add_node(found_node, q);
    }
    return;
}
```
```

The **insert_after** function adds a node, containing val2 in its data field, after the node containing val1 in its data field. The function first invokes **find_node** to locate the node containing val1 and creates a new node containing val2. Finally, **insert_after** calls **add_node** to link the pointers of the two nodes.

# ### 16.14.5 The delete_node Function

```
```c
void delete_node(struct node **head, short val)
{
    struct node *found_node, *current;
    found_node = find_node(*head, val);
    if (found_node == NULL)
        printf("Search value not found\n");
    else {
        current = *head;
        while (current->next != found_node)      /* Locates predecessor node */
            current = current->next;

        if (found_node == *head)
            *head = found_node->next;
        else
            current->next = found_node->next;
        free(found_node);
    }
    return;
}
```
```

This function deletes the node containing val in its data field. It first invokes **find_node** to locate the node to be deleted. For deleting a node, it is also necessary to know its predecessor and link it with the node following the deleted one. Depending on whether the deletion occurs at the beginning of the list or later, the *next* pointer of **found_node** is assigned to either `*head` or `current->next`. The memory allocated for the deleted node is finally freed and returned to the heap.