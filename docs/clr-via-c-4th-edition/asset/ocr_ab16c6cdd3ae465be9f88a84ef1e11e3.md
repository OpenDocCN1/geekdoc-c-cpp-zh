item, then a Monitor is taken internally to extract an item from another thread's mini-collection. We say that the thread is stealing the item from another thread.

You'll notice that all the concurrent classes offer a GetEnumerator method, which is typically used with C#'s foreach statement, but can also be used with Language Integrated Query (LINQ). For the ConcurrentStack, ConcurrentQueue, and ConcurrentBag, the GetEnumerator method takes a snapshot of the collection's contents and returns elements from this snapshot; the contents of the actual collection may change while enumerating over the snapshot. ConcurrentDictionary's GetEnumerator method does not take a snapshot of its contents, so the contents of the dictionary may change while enumerating over the dictionary; beware of this. Also note that the Count property returns the number of elements that are in the collection at the moment you query it. The count may immediately become incorrect if other threads are adding or removing elements from the collection at the same time.

Three of the concurrent collection classes, ConcurrentStack, ConcurrentQueue, and ConcurrentBag, implement the IProducerConsumerCollection interface, which is defined as follows.

```
    public interface IProducerConsumerCollection<T> : IEnumerable<T>, ICollection, IEnumerable {
       Boolean TryAdd(T item);
       Boolean TryTake(out T item);
       T[] ToArray();
       void CopyTo(T[] array, Int32 index);
    }
```

Any class that implements this interface can be turned into a blocking collection, where threads producing (adding) items will block if the collection is full and threads consuming (removing) items will block if the collection is empty. Of course, I'd try to avoid using blocking collections because their purpose in life is to block threads. To turn a non-blocking collection into a blocking collection, you construct a System.Collections.Concurrent.BlockingCollection class by passing in a reference to a non-blocking collection to its constructor. The BlockingCollection class looks like this (some methods are not shown).

```
    public class BlockingCollection<T> : IEnumerable<T>, ICollection, IEnumerable, IDisposable {
       public BlockingCollection(IProducerConsumerCollection<T> collection,
          Int32 boundedCapacity);

       public void Add(T item);
       public Boolean TryAdd(T item, Int32 msTimeout, CancellationToken cancellationToken);
       public void CompleteAdding();

       public T Take();
       public Boolean TryTake(out T item, Int32 msTimeout, CancellationToken cancellationToken);

       public Int32  BoundedCapacity  { get; }
       public Int32  Count            { get; }
       public Boolean IsAddingCompleted { get; }  // true if CompleteAdding is called
       public Boolean IsCompleted       { get; }  // true if IsAddingComplete is true and Count==0

       public IEnumerable<T> GetConsumingEnumerable(CancellationToken cancellationToken);
    }
```