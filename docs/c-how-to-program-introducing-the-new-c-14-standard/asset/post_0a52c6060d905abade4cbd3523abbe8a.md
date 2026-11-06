
arrows in part (b) illustrate *Step 4* of function `insertAtBack` that enables a new node to be added to the end of a list that’s not empty.

## 19.3.6 Member Function `removeFromFront`

Function `removeFromFront` (Fig. 19.5, lines 58–76) removes the front node of the list and copies the node value to the reference parameter. The function returns `false` if an attempt is made to remove a node from an empty list (lines 59–61) and returns `true` if the removal is successful. The function consists of several steps:

- 1. Initialize `tempPtr` with the address to which `firstPtr` points (line 63). Eventually, `tempPtr` will be used to delete the node being removed.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2298_0.png)

Fig. 19.7 Operation `insertAtBack` represented graphically.

- 2. If `firstPtr` is equal to `lastPtr` (line 65), i.e., if the list has only one element prior to the removal attempt, then set `firstPtr` and `lastPtr` to `nullptr` (line 66) to dethread that node from the list (leaving the list empty).
- 3. If the list has more than one node prior to removal, then leave `lastPtr` as is and set `firstPtr` to `firstPtr->nextPtr` (line 69; i.e., modify `firstPtr` to point to what was the second node prior to removal (and is now the new first node).
- 4. After all these pointer manipulations are complete, copy to reference parameter `value` the `data` member of the node being removed (line 72).
- 5. Now `delete` the node pointed to by `tempPtr` (line 73).
- 6. Return `true`, indicating successful removal (line 74).

**Figure 19.8** illustrates function `removeFromFront`. Part (a) illustrates the list before the removal operation. Part (b) shows the actual pointer manipulations for removing the front node from a nonempty list.

## 19.3.7 Member Function `removeFromBack`

Function `removeFromBack` (**Fig. 19.5, lines 79–105**) removes the back node of the list and copies the node value to the reference parameter. The function returns `false` if an attempt is made to remove a node from an empty list (lines 80–82) and returns `true` if the removal is successful. The function consists of several steps:

- 1. Initialize `tempPtr` with the address to which `lastPtr` points (line 84). Eventually, `tempPtr` will be used to delete the node being removed.
- 2. If `firstPtr` is equal to `lastPtr` (line 86), i.e., if the list has only one element prior to the removal attempt, then set `firstPtr` and `lastPtr` to `nullptr` (line 87) to dethread that node from the list (leaving the list empty).

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2301_0.png)

Fig. 19.8 Operation `removeFromFront` represented graphically.

- 3. If the list has more than one node prior to removal, then initialize `currentPtr` with the address to which `firstPtr` points (line 90) to prepare to “walk the list.”
- 4. Now “walk the list” with `currentPtr` until it points to the node before the last node. This node will become the last node after the remove operation completes. This is done with a `while` loop (lines 93–95) that keeps replacing `currentPtr` by `currentPtr->nextPtr`, while `currentPtr->nextPtr` is not `lastPtr`.
- 5. Assign `lastPtr` to the address to which `currentPtr` points (line 97) to dethread the back node from the list.
- 6. Set `currentPtr->nextPtr` to `nullptr` (line 98) in the new last node of the list.
- 7. After all the pointer manipulations are complete, copy to reference parameter `value` the `data` member of the node being removed (line 101).
- 8. Now `delete` the node pointed to by `tempPtr` (line 102).
- 9. Return `true` (line 103), indicating successful removal.

**Figure 19.9** illustrates `removeFromBack`. Part (a) of the figure illustrates the list before the removal operation. Part (b) of the figure shows the actual pointer manipulations.

## 19.3.8 Member Function `print`

Function `print` (Fig. 19.5, lines 113–129) first determines whether the list is *empty* (line 114). If so, it prints `"The list is empty"` and returns (lines 115–116). Otherwise, it outputs the value in each node. The function initializes `currentPtr` with `firstPtr` (line 119), then prints the string `"The list is: "` (line 121). While `currentPtr` is not `nullptr` (line 123), `currentPtr->data` is printed (line 124) and `currentPtr` is assigned the value of `currentPtr->nextPtr` (line 125). Note that if the link in the last node of the list does not have the value `nullptr`, the printing algorithm will erroneously attempt to print past the end of the list. Our printing algorithm here is identical for linked lists, stacks and queues (because we base each of these data structures on the same linked list infrastructure).

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2303_0.png)

Fig. 19.9 Operation `removeFromBack` represented graphically.

## 19.3.9 Circular Linked Lists and Double Linked Lists

The kind of linked list we’ve been discussing is a **singly linked list**—the list begins with a pointer to the first node, and each node contains a pointer to the next node “in sequence.” This list terminates with a node whose pointer member has the value `nullptr`. A singly linked list may be traversed in only one direction.

A **circular, singly linked list** ([Fig. 19.10](#)) begins with a pointer to the first node, and each node contains a pointer to the next node. The “last node” does not contain `nullptr`; rather, the pointer in the last node points back to the first node, thus closing the “circle.”

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2305_0.png)

**Fig. 19.10 Circular, singly linked list.**

A **doubly linked list** ([Fig. 19.11](#))—such as the Standard Library `list` class template—allows traversals *both forward and backward*. Such a list is often implemented with two “start pointers”—one that points to the first element of the list to allow *front-to-back traversal* of the list and one that points to the last element to allow *back-to-front traversal*. Each node has *both* a *forward pointer* to the next node in the list in the forward direction *and* a *backward pointer* to the next node in the list in the backward direction. If your list contains an alphabetized telephone directory, for example, a search for someone whose name begins with a letter near the front of the alphabet might best begin from the front of the list. Searching for someone whose name begins with a letter near the end of the alphabet might best begin from the back of the list.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2306_0.png)

Fig. 19.11 Doubly linked list.

In a circular, doubly linked list (*Fig. 19.12*), the *forward pointer* of the last node points to the first node, and the *backward pointer* of the first node points to the last node, thus closing the “circle.”

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_2306_1.png)

Fig. 19.12 Circular, doubly linked list.

## 19.4 Stacks

You learned the concept of a stack in [Section 6.11], [Section 15.7.1] (`stack` adapter) and [Section 18.2]. Recall that a node can be added to a stack and removed from a stack only at its *top*, so a stack is referred to as a *last-in, first-out (LIFO)* data structure. One way to implement a stack is as a *constrained version* of a linked list. In such an implementation, the link member in the last node of the stack is set to `nullptr` to indicate the *bottom* of the stack.

The primary member functions used to manipulate a stack are `push` and `pop`. Function `push` *inserts* a new node at the top of the stack. Function `pop` *removes* a node from the top of the stack, stores the popped value in a reference variable that’s passed to the calling function and returns `true` if the `pop` operation was successful (`false` otherwise).

### Applications of Stacks

Stacks have many interesting applications:

- In [Section 6.11], you learned that when a function call is made, the called function must know how to return to its caller, so the return address is pushed onto a stack. If a series of function calls occurs, the successive return values are pushed onto the stack in last-in,
