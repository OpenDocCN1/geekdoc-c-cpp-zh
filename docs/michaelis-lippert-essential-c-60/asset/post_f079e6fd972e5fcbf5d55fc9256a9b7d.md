
In summary, you should use a per-synchronization context instance of type object for the lock target.

## Guidelines

- AVOID locking on this, typeof(), or a string.
- DO declare a separate, read-only synchronization variable of type object for the synchronization target.

## ADVANCED TOPIC

### Avoid Synchronizing with MethodImplAttribute

One synchronization mechanism that was introduced in .NET 1.0 was the MethodImplAttribute. Used in conjunction with the MethodImplOptions.Synchronized method, this attribute marks a method as synchronized so that only one thread can execute the method at a time. To achieve this, the just-in-time compiler essentially treats the method as though it was surrounded by lock(this) or, in the case of a static method, locks on the type. Such an implementation means that, in fact, the method and all other methods on the same class, decorated with the same attribute and enum parameter, are synchronized—rather than each method being synchronized relative to itself. In other words, given two or more methods on the same class decorated with the attribute, only one of them will be able to execute at a time and the one executing will block all calls by other threads to itself or to any other method in the class with the same decoration. Furthermore, since the synchronization is on this (or even worse, on the type), it suffers the same detriments as lock(this) (or worse, for the static) discussed in the preceding section. As a result, it is a best practice to avoid the attribute altogether.

### Guidelines

- AVOID using the MethodImplAttribute for synchronization.

## Declaring Fields As volatile

On occasion, the compiler or CPU may optimize code in such a way that the instructions do not occur in the exact order they are coded, or some instructions are optimized out. Such optimizations are innocuous when code executes on one thread. However, with multiple threads, such optimizations may have unintended consequences because the optimizations may change the order of execution of a field’s read or write operations relative to an alternate thread’s access to the same field.

One way to stabilize this behavior is to declare fields using the volatile keyword. This keyword forces all reads and writes to the volatile field to occur at the exact location the code identifies instead of at some other location that the optimization produces. The volatile modifier identifies that the field is susceptible to modification by the hardware, operating system, or another thread. As such, the data is “volatile,” and the keyword instructs the compilers and runtime to handle it more exactly. (See http://bit.ly/CSharpReorderingOptimizations for further details.)

In general, the use of the volatile modifier is rare and fraught with complications that will likely lead to incorrect usage. Using lock is preferred to the volatile modifier unless you are absolutely certain about the volatile usage.

## Using the System.Threading.Interlocked Class

The mutual exclusion pattern described so far provides the minimum set of tools for handling synchronization within a process (application domain). However, synchronization with System.Threading.Monitor is a relatively expensive operation, and an alternative solution that the processor supports directly targets specific synchronization patterns.

Listing 19.6 sets _Data to a new value as long as the preceding value was null. As indicated by the method name, this pattern is the compare/exchange pattern. Instead of manually placing a lock around behaviorally equivalent compare and exchange code, the Interlocked.CompareExchange() method provides a built-in method for a synchronous operation that does the same check for a value (null) and updates the first parameter if the value is equal to the second parameter. Table 19.2 shows other synchronization methods supported by Interlocked.

Although it requires more code, thread-safe delegate invocation prior to C# 6.0 isn’t especially difficult, either. This approach works because the operators for adding and removing listeners are thread-safe and static (operator overloading is done with static methods). To correct Listing 19.7 and make it thread-safe, assign a copy, check the copy for null, and fire the copy (see Listing 19.8).

**LISTING 19.8: Thread-Safe Event Notification**

```
// ...
TemperatureChangedHandler localOnChange =
    OnTemperatureChanged;
if(localOnChange != null)
{
    // Call subscribers
    localOnChange(
        this, new TemperatureEventArgs(value) );
}
// ...
```

Given that a delegate is a reference type, it is perhaps surprising that assigning a local variable and then firing with the local variable is sufficient for making the null check thread-safe. As localOnChange points to the same location that OnTemperatureChanged points to, you might think that any changes in OnTemperatureChanged would be reflected in localOnChange as well.

However, this is not the case: Any calls to `OnTemperatureChanged += <listener>` will not add a new delegate to OnTemperatureChanged, but rather will assign it an entirely new multicast delegate without having any effect on the original multicast delegate to which localOnChange also points. This makes the code thread-safe because only one thread will access the localOnChange instance, and OnTemperatureChanged will be an entirely new instance if listeners are added or removed.

## Synchronization Design Best Practices

Along with the complexities of multithreaded programming come several best practices for handling those complexities.

### Avoiding Deadlock

With the introduction of synchronization comes the potential for deadlock. Deadlock occurs when two or more threads wait for one another to release a synchronization lock. For example, suppose Thread 1 requests a lock on _Sync1, and then later requests a lock on _Sync2 before releasing the lock on _Sync1. At the same time, Thread 2 requests a lock on _Sync2, followed by a lock on _Sync1, before releasing the lock on _Sync2. This sets the stage for the deadlock. The deadlock actually occurs if both Thread 1 and Thread 2 successfully acquire their initial locks (_Sync1 and _Sync2, respectively) before obtaining their second locks.

For a deadlock to occur, four fundamental conditions must be met:

1. **Mutual exclusion:** One thread (ThreadA) exclusively owns a resource such that no other thread (ThreadB) can acquire the same resource.
2. **Hold and wait:** One thread (ThreadA) with a mutual exclusion is waiting to acquire a resource held by another thread (ThreadB).
3. **No preemption:** The resource held by a thread (ThreadA) cannot be forcibly removed (ThreadA needs to release its own locked resource).
4. **Circular wait condition:** Two or more threads form a circular chain such that they lock on the same two or more resources and each waits on the resource held by the next thread in the chain.

Removing any one of these conditions will prevent the deadlock.

A scenario likely to cause a deadlock is when two or more threads request exclusive ownership on the same two or more synchronization targets (resources) and the locks are requested in different orders. This situation can be avoided when developers are careful to ensure that multiple lock acquisitions always occur in the same order. Another cause of a deadlock is locks that are not reentrant. When a lock from one thread can block the same thread—that is, when it re-requests the same lock—the lock is not reentrant. For example, if ThreadA acquires a lock and then re-requests the same lock but is blocked because the lock is already owned (by itself), the lock is not reentrant and the additional request will deadlock. Therefore, locks that are not reentrant can occur only with a single thread.

The code generated by the lock keyword (with the underlying Monitor class) is reentrant. However, as we shall see in the “More Synchronization Types” section, some lock types are not reentrant.

### When to Provide Synchronization

As we discussed earlier, all static data should be thread-safe. Therefore, synchronization needs to surround static data that is mutable. Generally, programmers should declare private static variables and then provide
