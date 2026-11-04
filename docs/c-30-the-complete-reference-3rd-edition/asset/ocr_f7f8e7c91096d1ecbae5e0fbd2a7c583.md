# The Semaphore

A semaphore is similar to a mutex except that it can grant more than one thread access to a shared resource at the same time. Thus, the semaphore is useful when a collection of resources is being synchronized. A semaphore controls access to a shared resource through the use of a counter. If the counter is greater than zero, then access is allowed. If it is zero, access is denied. What the counter is counting are permits. Thus, to access the resource, a thread must be granted a permit from the semaphore.

In general, to use a semaphore, the thread that wants access to the shared resource tries to acquire a permit. If the semaphore's counter is greater than zero, the thread acquires a permit, which causes the semaphore's count to be decremented. Otherwise, the thread will block until a permit can be acquired. When the thread no longer needs access to the shared resource, it releases the permit, which causes the semaphore's count to be incremented. If there is another thread waiting for a permit, then that thread will acquire a permit at that time. The number of simultaneous accesses permitted is specified when the semaphore is created. If you create a semaphore that allows only one access, then a semaphore acts just like a mutex.

Semaphores are especially useful in situations in which a shared resource consists of a group or pool. For example, a collection of network connections, any of which can be used for communication, is a resource pool. A thread needing a network connection doesn't care which one it gets. In this case, a semaphore offers a convenient mechanism to manage access to the connections.

The semaphore is implemented by System.Threading.Semaphore. It has several constructors. The simplest form is shown here:

```
```csharp
public Semaphore(int initial, int max)
```
```

Here, initial specifies the initial value of the semaphore permit counter, which is the number of permits available. The maximum value of the counter is passed in max. Thus, max represents the maximum number of permits that can granted by the semaphore. The value in initial specifies how many of these permits are initially available.

Using a semaphore is similar to using a mutex, described earlier. To acquire access, your code will call WaitOne() on the semaphore. This method is inherited by Semaphore from the WaitHandle class. WaitOne() waits until the semaphore on which it is called can be acquired. Thus, it blocks execution of the calling thread until the specified semaphore can grant permission.

When your code no longer needs ownership of the semaphore, it releases it by calling Release(), which is shown here:

```
```csharp
public int Release()
public int Release(int num)
```
```

The first form releases one permit. The second form releases the number of permits specified by num. Both return the permit count that existed prior to the release.

It is possible for a thread to call WaitOne() more than once before calling Release(). However, the number of calls to WaitOne() must be balanced by the same number of calls to Release() before the permit is released. Alternatively, you can call the Release(int) form, passing a number equal to the number of times that WaitOne() was called.