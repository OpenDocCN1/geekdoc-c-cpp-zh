
Notice that we have already copied the first node of the linked list. During the first iteration of the loop, we copy the second node of the linked list—the node that is pointed to by source_ptr. The first part of copying the node is a call to one of our other tools, list_insert, as shown here:

```
list_insert(tail_ptr, source_ptr->data());
```

This function call adds a new node to the end of the list that we are creating (i.e., after the node pointed to by tail_ptr), and the data in the new node is the number 20 (i.e., the data from source_ptr->data()). Immediately after the insertion, the function's pointers look like this:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_276_0.png)

The second statement in the loop body moves tail_ptr forward to the new tail of the new list, as shown here:

```
tail_ptr = tail_ptr->link();
```

This is the usual way that we make a pointer “move to the next node,” as we have seen in other functions such as list_search. After moving the tail pointer, the function’s pointers are configured as shown next:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_276_1.png)

In this example, source_ptr will move to the third node, and the body of the loop will execute one more time to copy the third node to the new list. Then the loop will end. The full implementation of list_copy is shown in Figure 5.8.

## FIGURE 5.8 Function for Copying a Linked List

### Function Implementation

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
    list_head_insert(head_ptr, source_ptr->data());
    tail_ptr = head_ptr;

    // Copy the rest of the nodes one at a time, adding at the tail of new list.
    source_ptr = source_ptr->link();
    while (source_ptr != NULL)
    {
        list_insert(tail_ptr, source_ptr->data()); // Loop for Step 4
        tail_ptr = tail_ptr->link();
        source_ptr = source_ptr->link();
    }
}
```

## Removing a Node at the Head of a Linked List

Our toolkit has three more functions, all of which remove nodes from a linked list. The first removal function removes the head node, as specified here:

```
void list_head_remove(node*& head_ptr);
// Precondition: head_ptr is the head pointer of a linked list,
// with at least one node.
// Postcondition: The head node has been removed and returned to the
// heap; head_ptr is now the head pointer of the new, shorter linked list.
```

As with list_head_insert, the head pointer is a reference parameter, since the function makes the head pointer point to a different node.

At first glance, it seems that the head node can be removed with just two steps: (1) Move the head pointer to the next node of the list; and (2) return the original head node to the heap. There is a small flaw with these steps: After we move the head pointer in Step 1, we no longer have any contact with the original head node. So, our complete pseudocode requires three steps:

- 1. Set a pointer named remove_ptr to point to the head node. (This is how we maintain contact with the original head node.)
- 2. Move the head pointer so that it points to the second node (or it becomes NULL if there is no second node).
- 3. delete remove_ptr. (This returns the original head node to the heap.)

These three steps are implemented in the top of Figure 5.9 on page 253.

## Removing a Node That Is Not at the Head

Our second removal function removes a node that is not at the head of a linked list. The approach is similar to inserting a node in the middle of a linked list. To remove a midlist node, we must set up a pointer to the node that is just before the node that we are removing. For example, to remove the 42 from the following list, we would need to set up previous_ptr as shown here:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_278_0.png)

As you can see, previous_ptr does not actually point to the node that we are deleting (the 42); instead it points to the node that is just before the condemned node. This is because the link field of the previous node must be reassigned, hence we need a pointer to this previous node. The removal function's prototype, using previous_ptr, is shown next.

```
void list_remove(node* previous_ptr);
// Precondition: previous_ptr points to a node in a linked list,
//   and this is not the tail node of the list.
// Postcondition: The node after previous_ptr has been removed
//   from the linked list.
```

The steps required by list_remove are similar to removing at the head of a list. Here is the pseudocode:

- 1. Set a pointer named `remove_ptr` to point to the condemned node. (This is the node after the one pointed to by `previous_ptr`.)
- 2. Reset the link field of `previous_ptr` so that it points to the node after the condemned node (or NULL if the condemned node is the tail node).
- 3. `delete remove_ptr`. (This returns the condemned node to the heap.)

As an example, let's remove the node 42 from the list that we just saw. The `previous_ptr` is set to point to the previous node, and then Step 1 of the removal pseudocode is executed. After Step 1, the pointers look like this:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_279_0.png)

Step 2 of the pseudocode needs to make the previous node's link point to the node that's after the node we are removing. This step changes the shaded pointer in the drawing shown here:

![](img/7bf56f684fab50d5ff9e94ae2818f3ac_279_1.png)

At this point, the node containing 42 is no longer part of the linked list. The list's first node contains 10, the next node has 20, and following the pointers we arrive at the third and last node, containing 30. All that remains is Step 3, `delete remove_ptr`, which returns the deleted node to the heap.

The complete implementation is shown in the middle part of Figure 5.9. You should check that the function works properly, even if the removed node is the last node of the list. In this case, the link of the previous node should be set to NULL, which occurs with no need for special code.

## Clearing a Linked List

Our final function removes all the nodes from a linked list, returning them to the heap. The implementation (`list_clear` in Figure 5.9) is a loop that repeatedly calls `list_head_remove` until all the nodes are gone. Notice that when the final node of the list is removed, the head pointer will be null, and this stops the loop. Also, the head pointer is a reference parameter, so that when the function returns, the actual head pointer in the calling program will be null.

## Linked-List Toolkit—Putting the Pieces Together

The functions of the toolkit are complete. Figure 5.10 on page 254 shows a header file for the toolkit, called node1.h. In addition to the documentation, the header file provides the class definition for the node, plus prototypes for the functions. In the file, we have defined the value_type to be a double, but as the documentation indicates, value_type may be changed to another data type.

## FIGURE 5.9 Functions for Removing Nodes from a Linked List

### Three Function Implementations

```
void list_head_remove(node*& head_ptr)
// Precondition: head_ptr is the head pointer of a linked list, with at least one node.
// Postcondition: The head node has been removed and returned to the heap;
// head_ptr is now the head pointer of the new, shorter linked list.
{
    node *remove_ptr;
    remove_ptr = head_ptr;
    head_ptr = head_ptr->link();
    delete remove_ptr;
}
```

```
void list_remove(node* previous_ptr)
// Precondition: previous_ptr points to a node in a linked list, and this is not the tail node of the list.
// Postcondition: The node after previous_ptr has been removed from the linked list.
{
    node *remove_ptr;
    remove_ptr = previous_ptr->link();
    previous_ptr->set_link(remove_ptr->link());
    delete remove_ptr;
}
```

```
void list_clear(node*& head_ptr)
// Precondition: head_ptr is the head pointer of a linked list.
// Postcondition: All nodes of the list have been deleted, and head_ptr is now NULL.
// Library facilities used: cstdlib
{
    while (head_ptr != NULL)
        list_head_remove(head_ptr);
}
```
