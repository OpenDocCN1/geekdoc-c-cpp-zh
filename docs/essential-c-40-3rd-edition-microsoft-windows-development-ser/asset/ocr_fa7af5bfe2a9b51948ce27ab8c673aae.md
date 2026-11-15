# Output 19.9:

```
12:19:36 AM: - 1
12:19:37 AM: - 2
12:19:38 AM: - 3
12:19:39 AM: - 4
12:19:40 AM: - 5
12:19:41 AM: - 6
12:19:42 AM: - 7
12:19:43 AM: - 8
12:19:44 AM: - 9
(Alarm Thread Id) 4 := 1 (Main Thread Id)
Final Count = 9
```

You can change the interval or time due after instantiation on System.Threading.Timer via the Change() method. However, you cannot change the callback listeners after instantiation. Instead, you must create a new instance.

# Asynchronous Programming Model

Multithreaded programming includes the following complexities:

+   1. Monitoring an asynchronous operation state for completion: This includes determining when an asynchronous operation has completed, preferably not by polling the thread's state or by blocking and waiting.
+   2. Thread pooling: This avoids the significant cost of starting and tearing down threads. In addition, thread pooling avoids the creation of too many threads, such that the system spends more time switching threads than running them.
+   3. Avoiding deadlocks: This involves preventing the occurrence of deadlocks while attempting to protect the data from simultaneous access by two different threads.
+   4. Providing atomicity across operations and synchronizing data access: Adding synchronization around groups of operations ensures that operations execute as a single unit and that they are appropriately interrupted by another thread. Locking is provided so that two different threads do not access the data simultaneously.