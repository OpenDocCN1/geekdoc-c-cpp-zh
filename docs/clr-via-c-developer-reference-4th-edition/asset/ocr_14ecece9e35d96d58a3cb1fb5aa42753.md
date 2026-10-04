```
public void CopyTo(T[] array, int index);
public T[] ToArray();
public void Dispose();

```

When you construct a BlockingCollection, the boundedCapacity parameter indicates the maximum number of items that you want in the collection. If a thread calls Add when the underlying collection has reached its capacity, the thread will block. If preferred, the threading can call TryAdd, a timeout (in milliseconds) and/or a CancellationToken, so the thread blocks until the item is added, the timeout expires, or the CancellationToken is canceled (see Chapter 27 for more information about the CancellationToken class).

The BlockingCollection implements the IDDisposable interface. If you call Dispose, it calls the underlying collection. It also disposes of two SemaphoreSlim objects that the class uses internally to block producers and consumers.

When you are not adding any more items into the collection, a producer should call the CompleteAdding method. This will signal the consumers that no more items will be produced. Specifically, this causes a foreach loop that is using GetConsumingEnumerable to terminate. The following example demonstrates how to set up a producer/consumer scenario and signal completion.

```
public static void Main() {
var bl = new BlockingCollection<Int32>(new ConcurrentQueue<Int32>());

// A thread pool thread will be consuming
ThreadPool.QueueUserWorkItem(ConsumeItems, bl);

// Add 5 items to the collection
for (Int32 item = 0; item < 5; item++) {
Console.WriteLine("Producing: " + item);
bl.Add(item);
}

// Tell the consuming thread(s) that no more items will be added to the collection
bl.CompleteAdding();

Console.ReadLine();   // For testing purposes
}
```

```
private static void ConsumeItems(Object o) {
var bl = (BlockingCollection<Int32>) o;

// Block until an item shows up, then process it
foreach (var item in bl.GetConsumingEnumerable()) {
Console.WriteLine("Consuming: " + item);
}
}
```

```
// The collection is empty and no more items are going into it
Console.WriteLine("All items have been consumed");
```