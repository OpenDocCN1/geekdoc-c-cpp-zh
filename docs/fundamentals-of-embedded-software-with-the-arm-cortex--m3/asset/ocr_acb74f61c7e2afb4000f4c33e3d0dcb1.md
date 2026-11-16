![](bbox=[0.26, 0.08, 0.82, 0.29])

FIGURE 10-5 Thread states in a non-preemptive kernel.

Non-preemptive systems have to make frequent kernel calls in order to achieve good response time. Threads running under a preemptive kernel, however, are not required to make kernel calls in order to yield. Context switching within the interrupt routine allows preemptive kernels to immediately activate the thread that processes the event. This provides a drastically improved and predictable response time that is critically important for real-time systems that depend on completion of their tasks within certain deadline constraints.

For example, Figure 10-6 illustrates how a preemptive system context switches from one thread to another when an interrupt occurs. Thread B is waiting in the pending state for some external event. As in the non-preemptive example of Figure 10-4, the event triggers an ISR that makes a semaphore post kernel call, changing the state of thread B from pending to ready. Just before returning, however, the ISR makes a second kernel call to the scheduler to check whether a context switch should occur, and changes the ISR's return address if necessary. As shown in Figures 10-5 and 10-7 both preemptive and non-preemptive kernels allow running threads to move temporarily to an “interrupted” state. Unlike non-preemptive kernels, however, a preemptive kernel allows the interrupted thread to move back to the ready state so that a different thread can resume when the interrupt is completed.

![](bbox=[0.26, 0.68, 0.82, 0.89])

FIGURE 10-6 Interrupt-triggered context switch in a preemptive kernel.