FIGURE 10-2 Initial thread state diagram.

![](bbox=[0.43, 0.08, 0.9, 0.33])

# 10.2 PENDING THREADS

To optimize processor utilization, scheduling must recognize that threads often have to wait for some event to occur or some shared resource to become available. When this happens, the scheduler should run a different thread while the first one waits. Simply moving the delayed task back into the ready state is not appropriate, however, because the thread may be selected to run again later, only to discover that it must continue to wait, thus adding unnecessary task switching overhead.

The solution is to introduce a fourth state called pending, shown in Figure 10-3.

When a running thread reaches a point where it cannot proceed until some specific condition is satisfied (such as the occurrence of an external event or the release of a shared resource), another kernel call is used to change the thread to the pending state; the scheduler then selects and runs one of the other threads from the ready list. When the pending condition is ultimately satisfied, another kernel call to the scheduler moves the pending thread to the ready state.

FIGURE 10-3 Revised thread state diagram.

![](bbox=[0.38, 0.66, 0.9, 0.91])