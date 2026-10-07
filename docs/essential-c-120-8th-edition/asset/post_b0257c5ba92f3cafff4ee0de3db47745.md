
# Using the System.Threading.Interlocked Class

The mutual exclusion pattern described so far provides the minimum set of tools for handling synchronization within a process (application domain). However, synchronization with System.Threading.Monitor is a relatively expensive operation, and an alternative solution that the processor supports directly targets synchronization patterns.

Listing 22.6 sets _Data to a new value as long as the preceding value was null. As indicated by the method name, this pattern is the compare/exchange pattern. Instead of placing a lock around behaviorally equivalent compare and exchange code, the Interlocked.CompareExchange() provides a built-in method for a synchronous operation that does the same for a value (null) and updates the first parameter if the value is equal to the second parameter. Table 22.2 shows other synchronization methods supported by Interlocked.

Listing 22.6: Synchronization Using System.Threading.Interlocked

```csharp
public class SynchronizationUsingInterlocked
{
    private static object? _Data;

    // Initialize data if not assigned
    public static void Initialize(object newValue)
    {
        // If _Data is null then set it to newValue
        Interlocked.CompareExchange(
            ref _Data, newValue, null);
    }
    
    // ...
}
```

# TABLE 22.2: Interlocked's Synchronization-Related Methods

| Method Signature | Description |
| :--- | :--- |
| public static T CompareExchange<T>(T location, T value, T comparand); | Checks location for the value in comparand. If the values are equal, it sets location to value and returns the original data stored in location. |

# Why Synchronization?

TABLE 22.2: Interlocked's Synchronization-Related Methods (continued)

| Method Signature | Description |
| :--- | :--- |
| public static T Exchange<T>(T location, T value); | Assigns location with value and returns previous value. |
| public static int Decrement(ref int location); | Decrements location by 1. It is equivalent to the -- operator, except that Decrement() is thread safe. |
| public static int Increment(ref int location); | Increments location by 1. It is equivalent to the ++ operator, except that Increment() is thread safe. |
| public static int Add(ref int location, int value); | Adds value to location and assigns location the result. It is equivalent to the += operator. |
| public static long Read(ref int location); | Returns a 64-bit value in a single atomic operation. |

Most of these methods are overloaded with additional data type signatures, as support for Long. Table 22.2 provides the general signatures and descriptions.
Note that you can use Increment() and Decrement() in place of the synchronized ++ and -- operators from Listing 22.5, and doing so will yield better performance. Also note that if a different thread accessed _Count using a non-interlocked method, the two accesses would not be synchronized.

# Event Notification with Multiple Threads

One area where developers overlook synchronization when firing events. The unsafe thread code for publishing an event is similar to Listing 22.7.

Listing 22.7: Firing an Event Notification

```csharp
// Thread safe
if (OnTemperatureChanged != null)
{
    // Call subscribers
    OnTemperatureChanged(
```

# Chapter 22: Thread Synchronization

```csharp
    this, new TemperatureEventArgs(value);
}
```

This code is valid as long as no race condition arises between this method and the event subscribers. However, the code is not atomic, so multiple threads could introduce a race condition. It is possible that between the time when OnTemperatureChange is checked for null and when the event is actually fired, OnTemperatureChange could be set to null, thereby throwing a NullReferenceException. In other words, if multiple threads could potentially access a delegate simultaneously, it is necessary to synchronize the assignment and firing of the delegate.

All that is necessary is to use the null-conditional operator:

```csharp
OnTemperature?.Invoke(
    this, new TemperatureEventArgs( value ));
```

The null-conditional operator is specifically designed to be atomic, so invocation of the delegate is, in fact atomic. The key—obviously—is to remember to make use of the null-conditional operator.

Although it requires more code, thread-safe delegate invocation isn’t especially difficult, either. This approach works because the operators for adding and removing listeners are thread safe and static (operator overloading is done with static methods). To correct Listing 22.7 and make it thread safe, assign the.

# Listing 22.8: Thread-Safe Event Notification

```csharp
// Thread safe
var handler = OnTemperatureChanged;
if (handler != null)
{
    // Call subscribers
    handler(this, new TemperatureEventArgs(value));
}
```

# Synchronization Design Practices

With the introduction of synchronization come several best practices for handling those complexities.

# Avoiding Deadlock

With the introduction of synchronization comes the potential for deadlock. Deadlock occurs when two or more threads wait for one another to release. For example, suppose Thread 1 requests a lock on _Sync1, and then requests a lock on _Sync2. At the same time, Thread 2 requests a lock on _Sync2, followed by a lock on _Sync1. This sets the stage for the deadlock. For a deadlock to occur, four fundamental conditions must be met:

- **Mutual exclusion**: One thread (Thread A) exclusively owns a resource that no other thread (Thread B) can acquire.
- **Hold and wait**: One thread (Thread A) with mutual exclusion is waiting to acquire a resource held by another thread (Thread B).
- **No preemption**: The resource held by a thread (Thread A) cannot be forcibly removed (Thread A needs to release its resource).
- **Circular wait condition**: Two or more threads form a circular chain that they lock on same or more resources, and each waits on the resource held by the next thread in the chain.

Removing any one of these conditions prevents the deadlock. One scenario likely to cause a deadlock when two or more threads request exclusive ownership on the same or more synchronization targets (resources) and the locks are requested in different orders. This situation can be avoided when developers are careful to ensure that multiple lock acquisitions always occur in the same order. Another potential cause of deadlock is locks that are not reentrant. When a lock from one thread can block the same thread—that is, when it re-requests the same lock—is blocked because the lock is already owned (by itself), it is not reentrant and the additional request will result in deadlock.

The code generated by the lock keyword (with the underlying Monitor class) is reentrant. However, as we shall see in the "More Synchronization Types" section, some lock types are not reentrant.

# When to Provide Synchronization

As discussed earlier, all static data should be thread safe. Therefore, synchronization needs to surround static data that is mutable. Generally, programmers should declare private variables and provide public methods for modifying the data. Such methods should internally handle the synchronization if multithreaded access is possible.

In contrast, instance state is not expected to include synchronization. Synchronization may significantly decrease performance and increase the chance of a lock contention or deadlock. With the exception of classes that are explicitly designed for multithreaded access, programmers sharing objects across multiple threads are expected to handle their own synchronization of the data being shared.
