Notice how well the analogy holds between the ADT stack and the stack of cafeteria plates. The operations that manipulate data on the ADT stack are the *only* such operations, and they correspond to the only things that you can do to a stack of plates. You can determine whether the stack of plates is empty but not how many plates are on the stack; you can inspect the top plate but no other plate; you can place a plate on top of the stack but at no other position; and you can remove a plate from the top of the stack but from no other position. If you were not permitted to perform any of these operations, or if you were permitted to perform any other operations, the ADT would not be a stack.

Although the stack of cafeteria plates suggests that, as you add or remove plates, the other plates move, do not have this expectation of the ADT stack. The stack operations involve only the top item and imply that only the other items in the stack remain in sequence. Implementations of the ADT stack operations might or might not move the stack's items. The implementations given in the next chapter do not move data items.

**Refining the specification of the ADT stack.** The following summary of the ADT stack provides some detail about how we wish to specify its operations. The names given here for stack operations are conventional.

| Data |
|---|
| • A finite number of objects, not necessarily distinct, having the same data type and ordered by when they were added. |

| Operations |
|---|
| Pseudocode | Description |
|---|---|
| isEmpty() | Task: Sees whether this stack is empty. Input: None. Output: True if the stack is empty; otherwise false. |
| push(newEntry) | Task: Adds newEntry to the top of this stack. Input: newEntry. Output: True if the operation is successful; otherwise false. |
| pop() | Task: Removes the top of this stack. That is, it removes the item that was added most recently. Input: None. Output: True if the operation is successful; otherwise false. |
| peek() | Task: Returns the top of this stack. That is, it gets the item that was added most recently. The operation does not change the stack. Input: None. Output: The top of the stack. |

Figure 6-2 shows a UML diagram for a class of stacks.

**Using the ADT stack in a solution.** Recall that Chapter 1 urged you to focus on the specification of a module before you considered its implementation. After writing an ADT's operations in