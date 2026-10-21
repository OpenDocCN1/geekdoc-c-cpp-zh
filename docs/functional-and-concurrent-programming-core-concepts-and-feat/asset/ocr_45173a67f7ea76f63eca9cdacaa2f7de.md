```
def put(element: A): Unit =
    lock.lock()
    try
        while queue.length == capacity do canPut.await()
        canTake.signal()
        queue.enqueue(element)
    finally lock.unlock()
```

Listing 23.8: Bounded queue based on two conditions.

Methods await, signal, and signalAll correspond to methods wait, notify, and notifyAll on intrinsic conditions. This implementation has better performance than Listing 23.7 because inserting or removing an element triggers the notification of at most one thread—using signal, not signalAll. Standard blocking queues from java.util.concurrent rely on a similar strategy—an instance of ReentrantLock and two conditions.

# Aside on Verification by Model Checking

Footnote 1 mentioned that using notify instead of notifyAll in Listing 23.7 could lead to a deadlock situation. This deadlock is not as systematic as it was in Listing 22.3—most runs proceed correctly to completion—and the steps it takes to make it happen are not entirely obvious. As an illustration of techniques that can be used to complement runtime testing, this aside applies model checking to the incorrect queue implementation—notifyAll replaced with notify—to discover the deadlock.

The formalism used here is TLA⁺, the Temporal Logic of Actions. It is a mathematical notation based on set theory, with some temporal logic elements added. A model of method put from a blocking queue can be written in TLA⁺ as follows:

Put(t, m) ≜ IF Len(queue) < Capacity
    THEN queue' = Append(queue, m) ∧ Notify
    ELSE Wait(t) ∧ UNCHANGED queue

The details are not essential, but it can be seen that the model uses the same strategy as in Listing 23.7, except that notify is used instead of notifyAll.ᵃ In particular, if the queue is not full, an element is added and method notify is called; otherwise, the thread calls method wait and the queue is unchanged. Method take is modeled similarly.

ᵃThe models uses IF instead of while because of an implicit loop in the TLA⁺ model, but the condition is being rechecked as in Listing 23.7.