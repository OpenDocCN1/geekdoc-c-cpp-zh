# Using a Mutex and a Semaphore

Although C#'s lock statement is sufficient for many synchronization needs, some situations, such as restricting access to a shared resource, are sometimes more conveniently handled by other synchronization mechanisms built into the .NET Framework. The two described here are related to each other: mutexes and semaphores.

# The Mutex

A mutex is a mutually exclusive synchronization object. This means it can be acquired by one and only one thread at a time. The mutex is designed for those situations in which a shared resource can be used by only one thread at a time. For example, imagine a log file that is shared by several processes, but only one process can write to that file at any one time. A mutex is the perfect synchronization device to handle this situation.

The mutex is supported by the System.Threading.Mutex class. It has several constructors. Two commonly used ones are shown here:

```
public Mutex()
public Mutex(bool owned)
```

The first version creates a mutex that is initially unowned. In the second version, if owned is true, the initial state of the mutex is owned by the calling thread. Otherwise, it is unowned.

To acquire the mutex, your code will call WaitOne() on the mutex. This method is inherited by Mutex from the Thread.WaitHandle class. Here is its simplest form:

```
public bool WaitOne();
```

It waits until the mutex on which it is called can be acquired. Thus, it blocks execution of the calling thread until the specified mutex is available. It always returns true.

When your code no longer needs ownership of the mutex, it releases it by calling ReleaseMutex(), shown here:

```
public void ReleaseMutex()
```

This releases the mutex on which it is called, enabling the mutex to be acquired by another thread.

To use a mutex to synchronize access to a shared resource, you will use WaitOne() and ReleaseMutex(), as shown in the following sequence:

```
Mutex myMtx = new Mutex();

// ...

myMtx.WaitOne(); // wait to acquire the mutex

// Access the shared resource.

myMtx.ReleaseMutex(); // release the mutex
```

When the call to WaitOne() takes place, execution of the thread will suspend until the mutex can be acquired. When the call to ReleaseMutex() takes place, the mutex is released and another thread can acquire it. Using this approach, access to a shared resource can be limited to one thread at a time.