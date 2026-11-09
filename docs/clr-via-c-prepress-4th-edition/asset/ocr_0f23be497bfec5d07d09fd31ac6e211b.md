```
```csharp
    Func<TKey, TValue> updateValueFactory);
    public TValue GetOrAdd(TKey key, TValue value);
    public Int32 Count { get; }
    public IEnumerator<KeyValuePair<TKey, TValue>> GetEnumerator();
}
```
```

All these collection classes are non-blocking. That is, if a thread tries to extract an element when no such element exists, the thread returns immediately; the thread does not block waiting for an element to appear. This is why methods like TryDequeue, TryPop, TryTake, and TryGetValue all return true if an item was obtained and returns false, if not.

These non-blocking collections are not necessarily lock-free. The ConcurrentDictionary class uses Monitor internally, but the lock is held for a very short time while manipulating the item in the collection. ConcurrentQueue and ConcurrentStack are lock-free; these both internally use Interlocked methods to manipulate the collection. A single ConcurrentBag object internally consists of a mini-collection object per thread. When a thread adds an item to the bag, Interlocked methods are used to add the item to the calling thread's mini-collection. When a thread tries to extract an element from the bag, the bag checks the calling thread's mini-collection for the item. If the item is there, then an Interlocked method is used to extract the item. If the thread's mini-collection doesn't have the item, then a Monitor is taken internally to extract an item from another thread's mini-collection. We say that the thread is stealing the item from another thread.

You'll notice that all the concurrent classes offer a GetEnumerator method, which is typically used with C#'s foreach statement, but can also be used with Language Integrated Query (LINQ). For the ConcurrentStack, ConcurrentQueue, and ConcurrentBag, the GetEnumerator method takes a snapshot of the collection's contents and returns elements from this snapshot; the contents of the actual collection may change while enumerating over the snapshot. ConcurrentDictionary's GetEnumerator method does not take a snapshot of its contents, so the contents of the dictionary may change while enumerating over the dictionary; beware of this. Also note that the Count property returns the number of elements that are in the collection at the moment you query it. The count may immediately become incorrect if other threads are adding or removing elements from the collection at the same time.

Three of the concurrent collection classes, ConcurrentStack, ConcurrentQueue, and ConcurrentBag, implement the IProducerConsumerCollection interface, which is defined as follows:

```
```csharp
public interface IProducerConsumerCollection<T> : IEnumerable<T>, ICollection, IEnumerable {
    Boolean TryAdd(T item);
    Boolean TryTake(out T item);
    T[] ToArray();
    void CopyTo(T[] array, Int32 index);
}
```
```

Any class that implements this interface can be turned into a blocking collection, where threads producing (adding) items will block if the collection is full and threads consuming (removing) items will block if the collection is empty. Of course, I'd try to avoid using blocking collections as their purpose in