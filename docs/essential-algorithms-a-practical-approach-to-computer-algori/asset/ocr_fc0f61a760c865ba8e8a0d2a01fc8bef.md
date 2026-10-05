# Chapter 5 - Stacks and Queues

The following pseudocode shows the algorithm for pushing an item onto an array-based stack:

```
Push(Data: stack_values [], Integer: next_index, Data: new_value)
  // Make sure there's room to add an item.
If (next_index == <length of stack_values>) Then <throw an exception>

  // Add the new item.
  stack_values[next_index] = new_value

  // Increment next_index.
  next_index = next_index + 1
End Push
```

The following pseudocode shows the algorithm for popping an item off an array-based stack:

```
Pop(Data: stack_values[], Integer: next_index)
  // Make sure there is an item to pop.
If (next_index == 0) Then <throw an exception>

  // Decrement next_index.
  next_index = next_index - 1

  // Return the top value.
  Return stack_values[next_index]
End Pop
```

Figure 5-3 shows the stack after the program has pushed the letters A, B, P, L, and E onto it. The middle image shows the stack after the new letter S has been pushed onto the stack. The bottom image shows the stack after the S has been popped off the stack.

With an array-based stack, adding and removing an item has O(1) times, both operations are quite fast. Setting and getting a value from array is generally faster than creating a new cell in a linked list. The array-based stack also doesn't need extra memory to store links between cells.

Unlike a linked-list stack, an array-based stack requires extra space to hold new items. How much extra space depends on your application and whether you know how many items might fit into the stack. If you don't know how many items you might need to store in the array, you can resize the array if needed, although that will take extra time. If the array holds N items when you need to resize it, it will take O(N) steps to copy those items into the newly resized array.

Depending on the how, an array occasionally needs to store 1,000 items in a stack, most of the time it stores only a few. In that case, most of the time the array will take up much more space than necessary. If you know