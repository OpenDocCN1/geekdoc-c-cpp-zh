# LOCKS

347

> ASIDE: MORE REASON TO AVOID SPINNING: PRIORITY INVERSION\One reason to avoid spin locks performance: as described in the main text, if a thread is interrupted while holding a lock, other threads that use spin locks will spend a large amount of CPU time just waiting for the lock to become available. However, it turns out there is another interesting reason to avoid spin locks on some systems: correctness. The problem to be wary of is known as priority inversion, which unfortunately is an interalgic scourge, occurring on Earth [15] and Mars [R97]!
Let's assume there are two threads in a system. Thread 2 (T2) has a high scheduling priority, and Thread 1 (T1) has lower priority. In this, let's assume the CPU scheduler will always run T2, if indeed both are runnable; T1 only runs when T2 is (e.g., when blocked on I/O).
Now, the problem. Assume T2 is blocked for some reason. So T1 runs, grabs a spin lock, and enters a critical section. T2 becomes unblocked (perhaps because an I/O completed), and the CPU immediately schedules it (thus scheduling T1). T2 tries to acquire the lock, and because it can't T1 holds the lock, it keeps spinning. Because it is a spin lock, T2 spins forever, and the system is hung.
Just avoiding the use of spin locks, unfortunately, does not avoid the problem of inversion (alse). Imagine three threads, T1, T2, and T3, at the highest priority, and T1 the lowest. Now that T3 grabs immediately (preempting T1), T3 starts waiting, because it is higher priority than T1, T1 runs immediately than T2, getting waiting, T3 tries to acquire the lock that T1 still holds. If T2 starts to run, it will have higher priority than T1, and thus will run. T3, which is higher priority than T2, is waiting because the mighty T3 can't run now that T2 is running. Isn't it sad that the mighty lowly T2 controls the CPU? Having high priority just not what it used to be.
You can address the priority inversion problem in a number of ways. In the specific case where spin locks cause the problem, you can avoid spin locks waiting (described more below). More generally, a higher-priority thread waiting for a lower-priority thread can temporarily boost the lower thread's priority, enabling it to run and overcoming the inversion, a technique known as priority inheritance. A last solution is simplest: ensure all threads have the same priority.

We do a couple of interesting things in this example. First, we combine the old test-and-set idea with an explicit lock waiters to make a more efficient lock. Second, we use a queue to help who gets the lock next and thus avoid starvation.

You might notice how the guard is used (Figure 28.9, page 346), basically as a spin-lock around the flag and queue manipulations the lock is using. This approach doesn't avoid spin-waiting entirely; a thread

© 2008–19, RPACI-DUSSEAU

# THREE
EASY
PIECES