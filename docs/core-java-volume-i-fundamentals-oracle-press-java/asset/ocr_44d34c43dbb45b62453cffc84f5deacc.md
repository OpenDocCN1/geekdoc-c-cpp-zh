change are tightly coupled. The only way to look up an element is to call next, and that lookup advances the position.

Instead, think of Java iterators as being *between elements*. When you call next, the iterator *jumps over* the next element, and it returns a reference to the element that it just passed (see Figure 9.3).

> **NOTE:**
> 
> Here is another useful analogy. You can think of `Iterator.next` as the equivalent of `InputStream.read`. Reading a byte from a stream automatically “consumes” the byte. The next call to `read` consumes and returns the next byte from the input. Similarly, repeated calls to `next` let you read all elements in a collection.

The `remove` method of the `Iterator` interface removes the element that was returned by the last call to `next`. In many situations, that makes sense—you need to see the element before you can decide that it is the one that should be removed. But if you want to remove an element in a particular position, you still need to skip past the element. For example, here is how you remove the first element in a collection of strings:

```
```java
Iterator<String>
it = c.iterator(); // skip over the first element
it.remove(); // now remove it
```
```