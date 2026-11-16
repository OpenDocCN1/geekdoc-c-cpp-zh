processor is needed whether a slower (and less expensive) one would suffice. As you might expect, as processor utilization increases, so does the probability that the tasks will not be able to meet their deadlines. A general rule of thumb is to try to keep utilization below 80%.

# 10.7 DEADLOCK

Deadlock is a situation in which two or more threads are blocked because they are waiting on each other's resources. It can occur only when each of these threads requires exclusive access to two or more shared resources simultaneously (Figure 10-11).

Consider two threads T1 and T2 that share two resources R1 and R2. Since the resources are shared, the threads use mutex objects M1 (for resource R1) and M2 (for resource R2) to protect their critical sections. Suppose that thread T1 has locked mutex M1 because it is using resource R1, and that thread T2 has locked mutex M2 because it is using R2. This corresponds to the beginning of Figure 10-12, where both threads are still active and neither is blocked.

The problem begins when each thread attempts to lock the other mutex without first unlocking the one it already owns. For example, when T2 attempts to lock M1, the kernel puts T2 into the pending state since M1 is already locked by T1. T1 continues to run but then attempts to lock M2; since M2 is already locked by T2, the kernel puts T1 into the pending state too. With both threads now blocked and pending, neither can complete its critical section in order to release its lock.

Our example was based on only two threads for simplicity. After a little thought, you will soon realize that an N-way deadlock with more than two threads is also possible (as in Figure 10-11). As N increases, our ability to recognize a potential deadlock

FIGURE 10-11 Deadlock.

![](bbox=[0.37, 0.6, 0.81, 0.91])