| `java.util.ListIterator<E>` | 1.2 |
|---|---|
| `void add(E newElement)` | adds an element before the current position. |
| `void set(E newElement)` | replaces the last element visited by `next` or `previous` with a new element. Throws an `IllegalStateException` if the list structure was modified since the last call to `next` or `previous`. |
| `boolean hasPrevious()` | returns true if there is another element to visit when iterating backwards through the list. |
| `E previous()` | returns the previous object. Throws a `NoSuchElementException` if the beginning of the list has been reached. |
| `int nextIndex()` | returns the index of the element that would be returned by the next call to `next`. |
| `int previousIndex()` | returns the index of the element that would be returned by the next call to `previous`. |

| `java.util.LinkedList<E>` | 1.2 |
|---|---|
| `LinkedList()` | constructs an empty linked list. |
| `LinkedList(Collection<? extends E> elements)` | constructs a linked list and adds all elements from a collection. |
| `void addFirst(E element)` |  |
| `void addLast(E element)` | adds an element to the beginning or the end of the list. |
| `E getFirst()` |  |
| `E getLast()` | returns the element at the beginning or the end of the list. |
| `E removeFirst()` |  |
| `E removeLast()` | removes and returns the element at the beginning or the end of the list. |