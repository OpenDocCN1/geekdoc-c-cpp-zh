
item, then a Monitor is taken internally to extract an item from another thread's mini-collection. We say that there is stealing the item from another thread.

You'll notice that all the concurrent classes offer a GetEnumerator method, which is typically used with C# foreach statement, but can also be used with Language Integrated Query (LINQ). For the ConcurrentStack, ConcurrentQueue, and ConcurrentBag, the GetEnumerator method takes a snapshot of the collection's contents and returns elements from this snapshot; the actual collection may change while enumerating the snapshot. ConcurrentDictionary's GetEnumerator does not take a snapshot of it, so the contents of the dictionary may change while enumerating over the dictionary; beware of this. Also note that the Count property returns the number of elements that are in the collection at the moment you call it. The count may immediately become incorrect if other threads are adding or removing elements from the collection at the same time.

Three of the concurrent classes, ConcurrentStack, ConcurrentQueue, and ConcurrentBag, implement the IProducerConsumer interface, which is defined as follows.

```csharp
public interface IProducerConsumerCollection<T> : IEnumerable<T>, ICollection, IEnumerable {
    Boolean TryAdd(T item);
    Boolean TryTake(out T item);
    T[] ToArray(T[] array, Int32 index);
    void CopyTo(T[] array, Int32 index);
}
```

Any class that implements this interface can be turned into a blocking collection, where threads producing (adding) items will block if the collection is full and threads (removing) items will block if the collection is empty. Of course, I'd try to avoid using blocking collections because their purpose is to block threads. To turn a non-blocking collection into a blocking collection, you construct a System.Collections.BlockingCollection by passing a reference to a non-blocking collection to its constructor. The BlockingCollection class looks like this (some methods are not shown).

```csharp
public class BlockingCollection<T> : IEnumerable<T>, IEnumerable, IDisposable {
    public BlockingCollection(IProducerConsumerCollection<T> collection, Int32 boundedCapacity);

    public void Add(T item);
    public Boolean TryAdd(T item, Int32 timeout, CancellationToken cancellationToken);
    public void CompleteAdding();

    public T Take();
    public Boolean TryTake(out T item, Int32 timeout, CancellationToken cancellationToken);

    public Int32 BoundedCapacity { get; set; }
    public Int32 Count { get; set; }
    public Boolean IsAddingCompleted { get; set; } // true if CompleteAdding is called
    public Boolean IsAddingComplete { get; set; } // true if IsAddingComplete is true and Count==0

    public IEnumerable<T> GetConsumingEnumerable(CancellationToken cancellationToken);

    public void CopyTo(T[] array, int index);
    public T[] ToArray();
    public void Dispose();
}
```

When you construct a BlockingCollection, the boundedCapacity parameter indicates the maximum number of items that you want in the collection. If a thread calls Add when the underlying collection has reached its capacity, the thread will block. If preferred, the threading can call TryAdd, a timeout (in milliseconds) and/or a CancellationToken, so the thread blocks until the item is added, the timeout expires, or the CancellationToken is canceled (see Chapter 27 for more information about the CancellationToken class).

The BlockingCollection implements the IDisposable interface. If you call Dispose, it calls the underlying collection. It also disposes of two SemaphoreSlim objects that the class uses internally to block producers and consumers.

When you are not adding any more items into the collection, a producer should call the CompleteAdding method. This will signal the consumers that no more items will be produced. Specifically, this causes a foreach loop that is using GetConsumingEnumerable to terminate. The following example demonstrates how to set up a producer/consumer scenario and signal completion.

```csharp
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

```csharp
private static void ConsumeItems(Object o) {
    var bl = (BlockingCollection<Int32>) o;

    // Block until an item shows up, then process it
    foreach (var item in bl.GetConsumingEnumerable()) {
        Console.WriteLine("Consuming: " + item);
    }
}
```

```csharp
// The collection is empty and no more items are going into it
Console.WriteLine("All items have been consumed");
```

When I execute the preceding code, I get the following output.

```
Producing: 0
Producing: 1
Producing: 2
Producing: 3
Producing: 4
Consuming: 0
Consuming: 1
Consuming: 2
Consuming: 3
Consuming: 4
All items have been consumed
```

If you run this yourself, the Producing and Consuming lines could be interspersed, but the All items have been consumed line will always be last.

The BlockingCollection class also has static AddToAny, TryAddToAny, TakeFromAny, and TryTakeFromAny methods. All of these methods take a BlockingCollection<T>[], in addition to an item, a timeout, and a CancellationToken. The (Try)AddToAny methods cycle through all the collections in the array until they find a collection that can accept the item because it is below capacity. The (Try)TakeFromAny methods cycle through all the collections in the array until they find a collection to remove an item.

## Symbols
- .NET Framework
- checking for, 8
- older code, 459
- reflection API, 583
- stability with, 34
- projections, 655
- version, 268
- WinRT interoperability with, 654, 655
- .winmd file extension, 644

A
- AbandonedMutex exception, 785
- Abort method, 579, 581
- Thread class, 679
- aborting threads, 578
- accessibility, 166
- accessibility modifiers, 156
- accessor resources, 505
- accessor methods, 228, 231
- accessibility of, 248
- generic, 248
- indexers, 244
- inlining, 247
- naming, 245
- performance of, 247
- AcquireReaderLock method, 355
- AcquireWriterLock method, 355

API for .NET Framework
- API for .NET Framework, 583
- APIs, WinRT, calling, 650
- AppDomain type, instance methods, 595
- AppDomainManager class, 576
- AppDomainMonitor class, 573
- AppDomains, 17
- aborting threads, 578
- accessing objects across boundaries, 559
- application output, 562
- ASP.NET applications and, 575
- assemblies in, 557
- assemblies in, discovering, 602
- assemblies using multiple, 573
- callback methods, 573
- confirming thread transitions between, 565
- CreateDomain method overloads, 563
- creating, 563
- default, 556
- definition of, 556
- demonstrations of, 563
- executable applications and, 574
- features of, 556
- first-chance exception notifications, 573
- foreground/background threads and, 688
- friendly names, 563
- garbage collection, 571
- garbage collection handle tables, 545
- graceful offsets, 577
- instance fields and, 566, 567
- isolation provided by, 557, 558, 566
- loading assemblies for specific, 585
- loading assemblies into, 564
- loading assemblies into multiple times, 586
- managed code and, 576
- marshaling objects by value, 568
- marshaling objects by references, 564
- memory usage, monitoring, 524
- method calls across boundaries, 566
- Microsoft Silverlight applications and, 574
- monitoring, 571
- passing objects across boundaries, 569
- permission set inheritance, 563
- proxy types, defining, 564
- purpose of, 553
- read-only properties in, 572
- robust host applications, 577
- singleton types and, 634
- SQL Server and, 575
- static members and, 567
- thread pools. see threads
- threads and, 562
- unloading, 477, 494, 566, 570
- unloading, as garbage collection trigger, 579
- XML web services applications and, 575
- AppDomainSetup object, 563
- Append method, 338
- AppChar method, 358
- AppDomainformat, 338, 345, 346, 347
- AppLine method, 538
- application developers, exception handling
- guidelines, and, 485
- application models, threading for, 748
- application state, serialization/deserialization
- of, 616
- application types, 36
- ApplicationException type, 466
- applications
- add-in support, 596
-ministrative control, 62
- AppDomains and, 574
- architecting for, 250
- compiling, 35
- configuration files, 62
- configuring for assembly download, 245
- dynamically extensible, 583, 888
- installation complexity, 34
- optimizing, 19
- single instance, 781
- ApplyPolicy method, 587
- .appx files, 60
