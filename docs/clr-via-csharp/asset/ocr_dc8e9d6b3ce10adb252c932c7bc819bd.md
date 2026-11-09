```
```csharp
            // The calling thread doesn't own the lock, wait for it
            m_lock.WaitOne();

            // The calling now owns the lock, initialize the owning thread ID & recursion count
            m_owningThreadId = currentThreadId;
            m_recursionCount--;
        }

        public void Leave() {
            // If the calling thread doesn't own the lock, we have an error
            if (m_owningThreadId != Thread.CurrentThread.ManagedThreadId)
                throw new InvalidOperationException();

            // Subtract 1 from the recursion count
            if (--m_recursionCount == 0) {
                // If the recursion count is 0, then no thread owns the lock
                m_owningThreadId = 0;
                m_lock.Set();    // Wake up 1 waiting thread (if any)
            }
        }

        public void Dispose() { m_lock.Dispose(); }
    }
```
```

While the behavior of the **RecursiveAutoResetEvent** class is identical to that of the **Mutex** class, a **RecursiveAutoResetEvent** object will have far superior performance when a thread tries to acquire the lock recursively because all the code that is required to track thread ownership and recursion is now in managed code. A thread has to transition into the Windows kernel only when first acquiring the **AutoResetEvent** or when finally relinquishing it to another thread.

# ## Calling a Method When a Single Kernel Construct Becomes Available

Having a thread block indefinitely waiting for a kernel object to become available is wasteful of the thread's memory resources. Therefore, the thread pool offers a way to invoke a method of yours when a kernel object becomes available by using the **System.Threading.ThreadPool** class's static **RegisterWaitForSingleObject** method. There are several overloads of this method, but they are all very similar. Here is the prototype for one of the more commonly used overloads:

```
```csharp
public static RegisteredWaitHandle RegisterWaitForSingleObject(
    WaitHandle waitObject, WaitOrTimerCallback callback, Object state,
    Int32 millisecondsTimeoutInterval, Boolean executeOnlyOnce);
```
```