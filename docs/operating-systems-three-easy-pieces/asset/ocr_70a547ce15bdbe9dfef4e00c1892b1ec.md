# COMMON CONCURRENCY PROBLEMS 413

(mtInit). When the initialization code runs, it sets the state of mtInit to 1 and signals that it has done. If Thread 2 had run before this point, it will be waiting for this signal and corresponding state; if it runs later, it will check the state and see that the initialization has already occurred (ie, mtInit is set to 1) and continues as is. Note that we could likely use mT as the variable itself, but do not do so for the sake of simplicity. When ordering matters between threads, condition variables (or semaphores) can come to the rescue.

# Non-Deadlock Bugs: Summary

A large fraction (97%) of non-deadlock bugs studied by Lu et al. are either atomicity or order violations. Thus, by carefully thinking about these types of bugs, programmers can likely do a better job of avoiding them. Moreover, as more automated code-checking tools develop, they should likely focus on these two types of bugs as they constitute a large fraction of non-deadlock bugs found in deployment.

Unfortunately, not all bugs are as fixed as the examples we looked at. Some require a deeper understanding of what the program is, or a larger amount of code or data structure reorganization to fix. Read Lu et al.’s (excellent and readable paper) for more details.

# 32.3 Deadlock Bugs

Beyond the concurrency bugs mentioned above, a classic problem that arises in modern systems with complex locking protocols is known as deadlock. Deadlock occurs, for example, when a thread (Thread 1) is holding a lock (L1) and waiting for another (L2); unfortunately, the thread (Thread 2) that is waiting for L2 to be released. Here is a code snippet that demonstrates a potential deadlock:

```
Thread 1:
pthread_mutex_lock(L1);
pthread_mutex_lock(L2);

Thread 2:
pthread_mutex_lock(L2);
pthread_mutex_lock(L1);
```

Figure 32.6: Simple Deadlock (deadlock .c)

Note that if code runs, deadlock does not necessarily occur; rather, it may occur, for example, Thread 1 grabs lock L1 and then a context switch to Thread 2. At that point, Thread 2 grabs L2, and tries to acquire L1. Thus we have a deadlock, as each thread is waiting for the other and neither can run. See Figure 32.7 for a graphical depiction; the presence of a cycle in the graph is indicative of the deadlock.

The figure should make the problem clear. How should programmers write code so to handle deadlock in some way?

© 2008–19, ARPACI-DUSSEAU

THREE
E
PIECES