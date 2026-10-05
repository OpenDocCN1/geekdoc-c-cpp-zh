If a task calls the Wait method and the result of decrementing the value of the SemaphoreSlim object would result in a negative value, the task waits until another task calls Release.

The SemaphoreSlim class also provides the CurrentCount property, which you can use to determine whether a Wait operation is likely to succeed immediately or will result in blocking.

# CountdownEvent

You can think of the CountdownEvent class as a cross between the inverse of a semaphore and a manual reset. When a task creates a CountdownEvent object, it specifies an initial value (a nonnegative integer). One or more tasks can call the Wait method of the CountdownEvent object, and its tasks are blocked. Wait does not decrement the value of the CountdownEvent object; instead, other tasks can call the Signal method to reduce the value. When the value of the CountdownEvent object reaches 0, all blocked tasks are signaled and can resume running.

A task can set the value of a CountdownEvent object back to the value specified in its constructor using the Reset method, and a task can increase this value by calling the AddCount method. You can determine whether a call to Wait is likely to block by examining the CurrentCount property.

# ReaderWriterLockSlim

The ReaderWriterLockSlim class is an advanced synchronization primitive that supports a single writer and multiple readers. The idea is that modifying (writing) to a resource requires exclusive access, but reading a resource does not. Multiple readers can access the same resource at the same time, but not at the same time as a writer.

A task that wants to read a resource calls the EnterReadLock method of the ReaderWriterLockSlim object. This action grabs a read lock on the object. When the task has finished with the resource, it calls the ExitReadLock method, which releases the read lock. Multiple tasks can read the same resource at the same time, and each task obtains its own read lock.

When a task modifies the resource, it can call the EnterWriteLock method of the ReaderWriterLockSlim object to obtain a write lock. If one or