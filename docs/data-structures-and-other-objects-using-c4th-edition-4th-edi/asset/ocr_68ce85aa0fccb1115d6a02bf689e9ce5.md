# FIGURE 5.8 Function for Copying a Linked List

# Function Implementation

```
void list_copy(const node* source_ptr, node*& head_ptr, node*& tail_ptr)
    // Precondition: source_ptr is the head pointer of a linked list.
    // Postcondition: head_ptr and tail_ptr are the head and tail pointers for a new list that contains
    // the same items as the list pointed to by source_ptr. NOTE: If there is insufficient
    // dynamic memory to create the new list, then bad_alloc is thrown.
    // Library facilities used: cstddef
{
    head_ptr = NULL;
    tail_ptr = NULL;

    // Handle the case of the empty list.
    if (source_ptr == NULL)
        return;

    // Make the head node for the newly created list, and put data in it.
    list_head_insert(head_ptr, source_ptr->data( ));
    tail_ptr = head_ptr;

    // Copy the rest of the nodes one at a time, adding at the tail of new list.
    source_ptr = source_ptr->link( );
    while (source_ptr != NULL)
    {
        list_insert(tail_ptr, source_ptr->data( ));      Loop for Step 4
        tail_ptr = tail_ptr->link( );
        source_ptr = source_ptr->link( );
    }
}
```

# Removing a Node at the Head of a Linked List

Our toolkit has three more functions, all of which remove nodes from a linked list. The first removal function removes the head node, as specified here:

```
void list_head_remove(node*& head_ptr);
// Precondition: head_ptr is the head pointer of a linked list,
// with at least one node.
// Postcondition: The head node has been removed and returned to the
// heap; head_ptr is now the head pointer of the new, shorter linked list.
```

As with list_head_insert, the head pointer is a reference parameter, since the function makes the head pointer point to a different node.