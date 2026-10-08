namespace are specially designed thread-safe collection classes that should be used in favor of their generic counterparts.

> **Thread-Safe Collections**  
Although these collection classes are thread-safe, this simply means that they won't produce undefined results when used from multiple threads. However, you still need to pay attention to locking and thread-safety concerns.

For example, using ConcurrentStack, you have no guarantee that the following code would succeed:

if (!stack.IsEmpty)
{
    stack.Pop();
}

Even in this example, you still need to lock the stack instance to make sure that no other thread can access it between the IsEmpty check and the Pop operation, as shown here:

lock(syncLock)
{
    if (!stack.IsEmpty)
    {
        stack.Pop();
    }
}

The concurrent collection classes are shown in Table 23.1.

# TABLE 23.1  Concurrent Collections

| Class | Description |
| :--- | :--- |
| BlockingCollection<T> | Provides blocking and bounding capabilities for thread-safe collections that implement IProducerConsumerCollection<T> |
| ConcurrentBag<T> | Represents a thread-safe, unordered collection of objects |
| ConcurrentDictionary<TKey, TValue> | Represents a thread-safe collection of key-value pairs |
| ConcurrentQueue<T> | Represents a thread-safe first in-first out (FIFO) collection |
| ConcurrentStack<T> | Represents a thread-safe last in-first out (LIFO) collection |