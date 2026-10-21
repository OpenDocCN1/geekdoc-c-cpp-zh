![](bbox=[0.22, 0.13, 0.78, 0.34])

# Figure 27.1 Possible loss of value from concurrent calls to push on a stack.

To avoid locking, you can change top to be an atomic reference and update it using CAS. This way, a failed CAS can be used to detect attempts to modify the stack concurrently:

```
import java.util.concurrent.atomic.AtomicReference

private class Node[A](val value: A, var next: Node[A])

final class Stack[A]:
  private val top = AtomicReference[Node[A]]()

  def peek: Option[A] = top.get match
    case null => None
    case node => Some(node.value)

  def push(value: A): Unit =
    val node = Node(value, top.get)
    while !top.compareAndSet(node.next, node) do node.next = top.get

@tailrec
def pop(): Option[A] = top.get match
  case null => None
  case node => if top.compareAndSet(node, node.next)
    then Some(node.value) else pop()
```

Listing 27.3: Lock-free implementation of a thread-safe stack (Treiber's algorithm).