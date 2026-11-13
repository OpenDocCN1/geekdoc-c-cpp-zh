# FIGURE 5.5 A Function to Compute the Length of a Linked List

# A Function Implementation

```
size_t list_length(const node* head_ptr)
// Precondition: head_ptr is the head pointer of a linked list.
// Postcondition: The value returned is the number of nodes in the linked list.
// Library facilities used: cstdlib
{
    const node *cursor;
    size_t answer;

    answer = 0;
    for (cursor = head_ptr; cursor != NULL; cursor = cursor->link( ))
    ++answer;
    return answer;
}
```

The complete implementation of the `list_length` function is shown in Figure 5.5. Notice that the local variable, `cursor`, is declared using the `const` keyword: `const node *cursor;`. This is required because the `head_ptr` parameter is const, so if `cursor` was not const, then the compiler would not permit the assignment `cursor = head_ptr`. In general, if a pointer is declared using the `const` keyword, then that pointer can be assigned only to another pointer that is also declared with the `const` keyword.

# HOW TO TRAVERSE A LINKED LIST

You should learn the important pattern for traversing a linked list, as used in the `list_length` function (Figure 5.5). The same pattern can be used whenever you need to step through the nodes of a linked list one at a time.

The first part of the pattern concerns moving from one node to another. Whenever we have a pointer that points to some node, and we want the pointer to point to the next node, we must use the link of the node. Here is the reasoning that we follow:

+   1. Suppose cursor points to some node;
+   2. Then cursor->link( ) points to the next node (if there is one), as shown here: