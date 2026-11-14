+   2. Flag Time
+   Flag time is determined from the execution time of the machine's bit test instruction.
+   Label this time \(\tau_f\).

+   3. Processing Time
+   Processing time is the time to perform the task associated with the triggering event. The triggering event may be either internal or external. This time must include the time to reach the flag from the current instruction. We make the assumption that we are in the polling loop and not at the test instruction. One must consider the best, worst, and average times. One must also include the time to reset the flag and to execute the task. We call this time \(\tau_p\).

One can consider anticipating the event if it is necessary to meet a very high-speed requirement with a slow causalous process or device. Anticipation is implemented by arming the system so that when an event occurs, everything is set up to go. One could use hardware as an implementing mechanism and consider a small window to respond to the event.

In computing the processing time, one must consider two cases, the first event and the nth event. For the first event, the loop is unburdened. In such a case, one has the minimum time to execute. If the loop permits events to queue, for the nth event time must be added to complete some subset of the n – 1 previous events. Such a time can be bounded by n – 1 times the time to process a single event.

# 14.12.2 Co-routine

In a noninterrupt environment, the time for a co-routine may be computed directly or, more often, bounded, which we compute as the worst case path through each component.

# 14.12.3 Interrupt-Driven Environment

An interrupt-driven environment is the most complex of the calculations because one is dealing with asynchronous events that can be nondeterministic. Events probably will not occur in the same sequence each time the program is executed. One can set a bound on the complexity of the computation by assuming only one such event can occur.

Several affecting factors include interrupt latency, the time for the context switch, the schedule, and the task execution time. For the context switch, the following times must be considered:

+   • Context switch to the interrupt handler.
+   • Acknowledging the interrupt.
+   • Context switch to the processing routine.
+   • Context switch back to the original context.

The schedule may be nonpreemptive or preemptive. A preemptive schedule with fixed rate scheduling is the easiest to compute. Let’s look at the pieces.

# 14.12.3.1 Preemptive Schedule

+   • Context Switch
+   The time for the context switch can be computed directly by identifying the instructions at the assembler level and counting the time each takes.