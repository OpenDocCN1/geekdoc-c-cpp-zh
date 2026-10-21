guarantees that if several threads call getAndSet(true) on a false Boolean, the method returns false for exactly one thread and true for all the other threads. Internally, getAndSet is implemented as a loop, using CAS.

The test isSet.get is not strictly necessary: It’s a performance optimization to avoid the more costly getAndSet if the Boolean is already true. The nonEmpty test on an option, which was necessary in Listing 22.4, is no longer used. The useless option is removed for performance reasons, and variable contents has now type A instead of Option[A].

# 27.2 Lock-Free Data Structures

Compare-and-set operations are not limited to primitive types such as integers and Booleans. Indeed, they are also available on references to objects as methods of the AtomicReference class. This makes it possible to update pointers atomically without locking, which is the basis of lock-free algorithms.

As an illustration, consider this lock-based implementation of a thread-safe stack:

```
Scala
private class Node[A](val value: A, val next: Node[A])

final class Stack[A]:
  private var top: Node[A] = null

  def peek: Option[A] = synchronized {
    if top == null then None else Some(top.value)
  }

  def push(value: A): Unit = synchronized {
    top = Node(value, top)
  }

  def pop(): Option[A] = synchronized {
    if top == null then None
    else
      val node = top
      top = node.next
      Some(node.value)
  }
```

You need locking to bring atomicity to push and pop. Without synchronization, two concurrent calls to push, for instance, could read the same top value and create two nodes, V1 and V2, that both refer to it (Figure 27.1). Then, if you update top to point to node V1, you lose the V2 value, and vice versa.