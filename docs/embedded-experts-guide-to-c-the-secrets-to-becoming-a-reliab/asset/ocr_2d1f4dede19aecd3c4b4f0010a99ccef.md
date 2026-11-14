```
/* Add the node to the end of the free
 * list. */
if (NULL != p_end_free)
{
/* If the free list is not empty, find the
 * last node of the free list and point it
 * to the freed node. */
while (NULL != p_end_free->p_next)
{
p_end_free = p_end_free->p_next;
}
p_end_free->p_next = p_node;
}
else
{
/* If the free list is empty, start a new
 * one. */
p_free_head = p_node;
}
}
```

Fig 3.2 The basic linked-list data structure is easy to implement. Each element in the list contains a pointer to the next element, which provides the “link” – the last link points to A doubly-linked list adds a link to the previous element to each entry. In a circular linked list, the list eventually loops back on itself – rather than linking to the last element links back to the first, although “first” and “last” essentially become meaningless in this case. Lists are typically intended only to contain one type, although type-generic implementations are possible.