acquire it, the latter piece of code will have to wait until the lock is released again. The idea of threads acquiring and releasing locks is shown in Figure 8.28.

![](bbox=[0.07, 0.18, 0.88, 0.73])

FIGURE 8.28 Mutual exclusion due to locking.

When the first thread starts its execution, it acquires the lock, which is fine because no other thread is currently holding it. The mechanics of acquiring a lock are shown later, but let's just focus on the conceptual diagram for now. Next, the thread starts its execution. Assuming a context switch occurs at the same time, as we've shown in our previous example (but that could vary, of course), the second thread gets scheduled and a context switch occurs.

Now the second thread starts by attempting to acquire the same lock as the first thread. Locks are put on resources that cannot be accessed simultaneously by different parties, so the same lock should be used by the different parties trying to access the protected resource. Because thread one already holds the lock, the request of thread two to acquire the lock fails. The second thread now enters a blocked state, and the threading infrastructure will decide to switch it off and give control to another thread. Thread two now effectively becomes “unschedulable” and won’t be considered for context switches until the lock is released. Ultimately, thread one, which isn’t blocked on anything, will get scheduled and can continue to run. Ultimately, it will release the lock, at which point the bookkeeping for threads will indicate that thread two now is schedulable because it no longer