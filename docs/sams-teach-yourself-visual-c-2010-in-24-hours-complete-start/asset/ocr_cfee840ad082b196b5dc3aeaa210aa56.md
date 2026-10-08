**12.** Run the application again using Ctrl+F5, and observe that the final output matches what is shown in Figure 9.11.

![](bbox=[0.25, 0.15, 0.66, 0.36])

![](bbox=[0.82, 0.15, 0.93, 0.2])

# Stacks and Queues

Stacks and queues are relatively simple collections that represent either a last-in-first-out (LIFO) collection or first-in-first-out (FIFO) collection. Even though these are simple collections, they are nevertheless very useful as well. Queues are useful for storing data in the order received for sequential processing, whereas stacks are useful for operations such as statement parsing. In general, stacks and queues are used when operations should be restricted to either the beginning or end of the list.

The Stack<T> class provides a stack implemented as an array in which operations always occur at the end of that array and can contain duplicate elements and null elements. Stack<T> provides a simple public interface, shown in Table 9.9.

TABLE 9.9 Common Members of Stack<T>

| Name | Description |
| :-- | :-- |
| Count | Gets the number of elements contained in the stack |
| Clear | Removes all elements from the stack |
| Contains | Determines if an element is in the stack |
| Peek | Returns the element at the top of the queue without removing it |
| Pop | Removes and returns the element at the top of the stack |
| Push | Inserts an element at the top of the stack |
| TrimExcess | Sets the capacity to the actual number of elements in the stack, if that number is less than 90% of the current capacity |