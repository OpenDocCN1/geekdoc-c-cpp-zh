# FIGURE 5.7 Implementations of Three Linked-List Functions

# Three Function Implementations

```
void list_insert(node* previous_ptr, const node::value_type& entry)
// Precondition: previous_ptr points to a node in a linked list.
// Postcondition: A new node containing the given entry has been added after the node that
// previous_ptr points to. NOTE: If there is insufficient dynamic memory for a new
// node, then bad_alloc is thrown before changing the list.
{
    node *insert_ptr;

    insert_ptr = new node;
    insert_ptr->set_data(entry);
    insert_ptr->set_link( previous_ptr->link( ) );
    previous_ptr->set_link(insert_ptr);
}
```

```
node* list_search(node* head_ptr, const node::value_type& target)
// Precondition: head_ptr is the head pointer of a linked list.
// Postcondition: The return value is a pointer to the first node containing the specified target in its
// data field. If there is no such node, the null pointer is returned.
// Library facilities used: cstdlib
{
    node *cursor;

    for (cursor = head_ptr; cursor != NULL; cursor = cursor->link( ))
        if (target == cursor->data( ))
            return cursor;
    return NULL;
}
```

```
const node* list_search(const node* head_ptr, const node::value_type& target)
// Precondition: head_ptr is the head pointer of a linked list.
// Postcondition: The return value is a pointer to the first node containing the specified target in its
// data field. If there is no such node, the null pointer is returned.
// Library facilities used: cstdlib
{
    const node *cursor;

    for (cursor = head_ptr; cursor != NULL; cursor = cursor->link( ))
        if (target == cursor->data( ))
            return cursor;
    return NULL;
}
```