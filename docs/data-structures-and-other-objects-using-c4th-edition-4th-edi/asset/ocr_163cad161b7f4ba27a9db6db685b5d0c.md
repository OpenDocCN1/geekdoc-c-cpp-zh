```
size_t list_length(const node* head_ptr);
```

The function uses the head pointer to access the list's nodes, but the function does not change any part of the list. In general, this is the situation when you should use `const node*`. A pointer to a constant node should be used when the function needs access to the linked list and the function will not make any changes to any of the list's nodes.

# Value parameters that are pointers to a node.

The second sort of node pointer parameter is a value parameter without the `const` keyword. For example, one of the toolkit's functions will add a new node after a specified node in the list. The function has this prototype with a `node*`:

```
void list_insert(node* p, const node::value_type& entry)
// Precondition: previous_ptr points to a node in a linked list.
// Postcondition: A new node containing the given entry has been added
// after the node that p points to.
```

The function uses the pointer p to access the list's nodes, and a new node is added after the p node. The pointer p will not change; it will stay pointing at the same node. But that node's link field will change and a new node will be added to the list. In general, this is the situation when you should use a value parameter: A node pointer should be a value parameter when the function needs access to the linked list, and the function might change the linked list, but the function does not need to make the pointer point to a new node.

# Reference parameters that are pointers to a node.

Sometimes a function must make a pointer point to a new node. For example, one of the toolkit functions will add a new node at the front of a linked list, with this prototype and precondition/postcondition contract:

```
void list_head_insert
(node*& head_ptr, const node::value_type& entry);
// Precondition: head_ptr is the head pointer of a linked list.
// Postcondition: A new node containing the given entry has been added at
// the head of the list; head_ptr now points to the head of the new, longer
// linked list.
```

The head_ptr is a reference parameter, since the function creates a new head node and makes the head pointer point to this new node. A node pointer should be a reference parameter when the function needs access to the linked list and the function makes the pointer point to a new node. This change to the pointer will make the actual argument point to a new node.