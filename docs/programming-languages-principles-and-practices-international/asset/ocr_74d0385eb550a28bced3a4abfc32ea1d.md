Assuming that such a TestAndSet operation returns the value of its location parameter and decrements its location parameter if it is > 0, we can implement Signal and Delay with the following code schemas:

```
Delay(S): while TestAndSet(S) <= 0 do {nothing};
Signal(S) : S := S + 1;
```

This implementation causes a blocked process to busy-wait or spin in a while-loop until S becomes positive again through a call to Signal by another process. (Semaphores implemented this way are sometimes called spin-locks.) It also leaves unresolved the order in which waiting processes are reactivated: It may be random or in some order imposed by the operating system. In the worst case, a waiting process may be preempted by many incoming calls to Delay from new processes and never get to execute despite a sufficient number of calls to Signal. Such a situation is called starvation. Starvation is prevented by the use of a scheduling system that is fair—that is, guarantees that every process will execute within a finite period of time. In general, avoiding starvation is a much more difficult problem to solve than avoidance of deadlock (which itself is not trivial). For example, neither Java nor Ada automatically provide for fair scheduling, although it is possible to achieve it with some effort. (See the Notes and References.)

Modern shared-memory systems often provide facilities for semaphores that do not require busy-waiting. Semaphores are special memory locations that can be accessed by only one processor at a time, and a queue is provided for each semaphore to store the processes that are waiting for it.

# 13.5 Monitors

A monitor is a language construct that attempts to encapsulate the mutual exclusion and synchronization mechanisms of semaphores. The idea is that a more structured construct will reduce programming errors and improve the readability and correctness of code. Originally designed by Per Brinch-Hansen and C. A. R. Hoare in the early 1970s, it has been used in the languages Concurrent Pascal and Mesa. It is also the basis for the concurrency mechanisms of both Java and Ada95, as you will see shortly.

A monitor is an abstract data type mechanism with the added property of mutual exclusion. It encapsulates shared data and operations on these data. At most one process at a time can be “inside” the monitor—using any of the monitor’s operations. To keep track of processes waiting to use its operations, a monitor has an associated wait queue, which is organized in some fair fashion (so that processes do not wait in the queue forever as other processes arrive)—for example, as a regular first in, first out queue.

A monitor, therefore, can be viewed as a language entity with the schematic structure shown in Figure 13.9.

![](bbox=[0.37, 0.74, 0.64, 0.86])

Figure 13.9 The structure of a monitor