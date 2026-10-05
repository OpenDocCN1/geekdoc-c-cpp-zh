22. Close CPU Stress.

23. Enter the following command to restore the system CPU set to its default:
Cpuset -s 0

# Thread selection on multiprocessor systems

Before covering multiprocessor systems in more detail, let's summarize the algorithms discussed earlier in the “Thread selection” section. They either continued executing the current thread (if no candidate was found) or started the idle thread (if the current had to block). However, there is a third algorithm for thread selection called SearchForNewThread, which was hinted earlier. This algorithm is called in one specific instance: when the current thread is about to block due to a wait on an object, including during an NtDelayExecutionThread call, also known as the S1leep API in Windows.

> Note This shows a difference between the commonly used S1leep call, which makes the thread block until the next timer, and the SwitchToThread call, which was shown earlier. The S1leep(1) call uses the algorithm about to be described, while the SwitchToThread call uses the previous logic.

KiSearchForNewThread initially checks whether there is already a thread that was selected for this processor (by reading the NextThread field). If so, it dispatches the thread immediately in the running state. Otherwise, it calls the KiSelectReadyThread routine and, if a thread was found, performs the steps.

If no thread was found, the processor is marked as idle (even though the idle thread is not yet executing) and a scan of the queues of other logical processors (shared) is initiated (unlike the other standard algorithms, which would give up). If, however, the processor core is parked, the algorithm will not attempt to check other logical processors, as it is preferable to allow the core to enter the parking state instead of keeping it busy with new work.

Barring these two scenarios, the work-stealing loop runs now. This code looks at current NUMA node and removes idle processors (because they shouldn't have threads that need stealing). The code looks at the current CPU's shared ready queue and calls KiSearchForNewThreadProcessor loop. If no thread is found, the affinity is changed to the next group and the function is called again. Again, however, the target CPU points it to the next group's shared queue instead of the current one, causing this processor to find the best thread from ready the other processor's ready queue. If this fails to find a thread to run, if DFS is enabled, a thread from the idle-only queue of the remote processor is released on the current processor, if possible.

If no ready thread is found, the next-lower numbered logical processor is attempted, and so on, until all logical processors have been exhausted on the current NUMA node.

CHAPTER 4 Threads 283