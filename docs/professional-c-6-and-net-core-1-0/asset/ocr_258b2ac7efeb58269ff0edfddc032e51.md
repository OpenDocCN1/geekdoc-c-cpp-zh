interfaces `IReadOnlyCollection<T>` and `IReadOnlyList<T>`. With the members of these interfaces, the collection cannot be changed.

# Queues

A queue is a collection whose elements are processed *first in, first out* (FIFO), meaning the item that is put first in the queue is read first. Examples of queues are standing in line at the airport, a human resources queue to process employee applicants, print jobs waiting to be processed in a print queue, and a thread waiting for the CPU in a round-robin fashion. Sometimes the elements of a queue differ in their priority. For example, in the queue at the airport, business passengers are processed before economy passengers. In this case, multiple queues can be used, one queue for each priority. At the airport this is easily handled with separate check-in queues for business and economy passengers. The same is true for print queues and threads. You can have an array or a list of queues whereby one item in the array stands for a priority. Within every array item there’s a queue, where processing happens using the FIFO principle.

> **NOTE** Later in this chapter, a different implementation with a linked list is used to define a list of priorities.

A queue is implemented with the `Queue<T>` class in the namespace `System.Collections.Generic`. Internally, the `Queue<T>` class uses an array of type `T`, similar to the `List<T>` type. It implements the interfaces `IEnumerable<T>` and `ICollection`, but it doesn’t implement `ICollection<T>` because this interface defines `Add` and `Remove` methods that shouldn’t be available for queues.

The `Queue<T>` class does not implement the interface `IList<T>`, so you cannot access the queue using an indexer. The queue just allows you to add an item to it, which is put at the end of the queue (with the `Enqueue` method), and to get items from the head of the queue (with the `Dequeue` method).

Figure 11.1 shows the items of a queue. The `Enqueue` method adds items to one end of the queue; the items are read and removed at the other end of the queue with the `Dequeue` method. Invoking the `Dequeue` method once more removes the next item from the queue.

![](bbox=[0.105, 0.747, 0.895, 0.815])

Figure 11.1

Methods of the `Queue<T>` class are described in the following table.