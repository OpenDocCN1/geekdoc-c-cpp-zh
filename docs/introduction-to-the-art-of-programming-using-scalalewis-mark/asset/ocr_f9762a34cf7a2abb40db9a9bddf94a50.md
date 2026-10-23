proper default values.¹ Type erasure takes away that information from the runtime. The manifest allows Scala to get back access to it.

It is also worth noting that our implementation of the stack technically does not actually remove the value from the array when pop() is called. This remove is not really required for the stack to execute properly. However, it can improve memory usage and performance, especially if the type A is large. Unfortunately, that would require having a default value to put into the array in that place, which we have just discussed it is hard from a completely general type parameter.

# 24.6 Array-Based Queue

Like the stack, the code for the array-based queue begins by setting up the ADT as a completely abstract trait. This trait, which takes a type parameter so that it can work with any type, is shown here.

```
package scalabook.adt

/**
 * This trait defines a mutable Queue ADT.
 * @tparam A the type of data stored
 */
trait Queue[A] {
  /**
   * Add an item to the queue.
   * @param obj the item to add
   */
  def enqueue(obj:A)

  /**
   * Remove the item that has been on the longest.
   * @return the item that was removed
   */
  def dequeue():A

  /**
   * Return the item that has been on the longest without removing it.
   * @return the most recently added item
   */
  def peek:A

  /**
   * Tells whether this queue is empty.
   * @return true if there are no items on the queue, otherwise false.
   */
  def isEmpty:Boolean
}
```

¹You also need other information such as how big a memory block should be reserved. For example, Int requires 4-bytes while Double requires 8.