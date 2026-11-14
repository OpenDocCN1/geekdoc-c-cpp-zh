
queue has a weight or relative priority which determines how many tasks in the queue will be scheduled before tasks in the next queue begin to be scheduled. For example, a scheduler using three queues may be implemented, with the first queue having a weight of 3, the second a weight of 2 and the third a weight of 1 – three tasks from the first queue could be scheduled, followed by two from the second queue and finally a single task from the third queue. As a result of the weighted scheduling, tasks in the first, high-priority queue will be allocated more overall processor time compared to tasks in the other two

| | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|
| Task #1 | | | | | | | |
| Task #2 | | | | | | | |
| Task #3 | | | | | | | |
| (a) Round Robin | | | | | | | |
| Task / Queue #1 (high priority) | | | | | | | |
| Task / Queue #2 (medium priority) | | | | | | | |
| Task / Queue #3 (low priority) | | | | | | | |
| (b) Weighted Round Robin | | | | | | | |
| Task / Queue #1 (high priority) | | | | | | | |
| Task / Queue #2 (medium priority) | | | | | | | |
| Task / Queue #3 (low priority) | | | | | | | |
| (c) Interleaved weighted Round Robin | | | | | | | |

Fig 10.3 - The simple round-robin scheduler (top) can be adapted to schedule tasks of different priorities. The weighted round-robin scheduler (centre) allocates more time to high-priority tasks, either by allowing them to run for longer or by allowing more tasks in the high-priority queue to run before switching to a lower priority task. The interleaved round-robin scheduler (bottom) achieves the same result, but distributes the time-slices for each priority so more evenly; although the total time spent running tasks in each queue is the same, some lower priority tasks will be allowed to run earlier than with the more basic weighted variety.

Using the UART, user input and display example introduced at the beginning of this chapter, we could choose to assign the highest priority to the UART servicing task, an intermediate priority to handling user input and a low priority to updating the display. This would allow the fast UART communications to be processed more frequently, while the display updates would only have to be processed occasionally. Assigning a medium priority to the user input allows this to be handled frequently enough for the user not to notice any significant delay.

This approach may seem intuitive and is likely to work for simple systems. However, a more thorough and systematic method of assigning priorities is required for most real systems. The optimal way to assign priorities, at least for fixed priority scheduling, is to use rate-monotonic scheduling. While correctly assigning priorities can require some in-depth analysis, the principle is straightforward – the less time a task requires, the higher its priority should be, much like the STCF approach discussed earlier. For optimal CPU usage, task periods should be harmonic – each period should be an exact multiple of the periods of higher-priority (shorter period) tasks. If tasks cannot be reliably scheduled using rate-monotonic scheduling, then they cannot be reliably scheduled using any fixed-priority scheduler.

In addition to requiring some thought be given to correctly assigning priorities to tasks, priority-based scheduling introduces a new risk to be wary of: priority inversion. This occurs when a high-priority task requires a resource currently being used by a low-priority task, which is subsequently pre-empted by a medium-priority task. The initial blocking of the high-priority task is not the problem: in this case, the scheduler has worked as intended. The problem occurs when the low-priority task is pre-empted by the medium-priority task; at this point, the high-priority task has also been pre-empted, albeit indirectly, in a way which does not respect task priorities.

More generally, multitasking either creates new potential issues or increases existing risks. For instance, stack overflow – where the call stack extends beyond its intended end and begins to read or write data never intended to be part of the stack – is always a potential problem; however, without multitasking this is rare and invariably indicates that the platform lacked the necessary memory to support the software; with multitasking, there can be plenty of memory available but a stack overflow may still occur if insufficient memory has been allocated to one (or more) of the individual task stacks. Conversely, deadlock – where two or more tasks are mutually dependent on the completion of each other and therefore prevented from progressing – is a problem which can only arise where multitasking is used.

In relatively simple multitasking environments such problems can be dealt with manually. Priority inversion can be avoided by using only one priority level for all tasks, allocated stack sizes can be increased providing sufficient total memory is available and best practice for preventing deadlocks is to only ever allow a task to hold a single mutex at a time, releasing the held mutex before attempting to acquire another (alternatively, if this is not possible, mutexes should only be acquired in a pre-defined order, and released if any of the acquisitions fail). However, as system complexity increases, an operating system quickly becomes an invaluable tool in managing the system.

Operating systems will be discussed in the next chapter.

## Endnotes for Chapter 10 - Multitasking

- 1 POSIX is the Portable Operating System Interface, the name given to the IEEE Computer Society’s operating system standards. It is heavily influenced by, and arguably a standardisation of, UNIX.
- 2 That is, restricted by design, not merely by usage, i.e. it is a static function within the module containing the thread.
- 3 It is possible to implement a very basic FIFO scheduler (sometimes referred to as a first come, first served, or FCFS scheduler) for multitasking. However, the real-world performance of such a basic scheduler makes them of relatively little practical use.
- 4 There are variations of the weighted round-robin algorithm which achieve the same overall result: the time tasks are allowed to run for could be determined from the priority of the task, for instance. A common alternative, the interleaved weighted round-robin scheduler, can be used to distribute processor time more evenly between queues without changing the overall time spent on individual tasks.
- 5 For continuously running tasks, the word complete may require some interpretation; a task that performs work in an infinite loop, for instance, might be considered complete each time it finishes one iteration.

## Chapter 11: Bootloaders and Operating Systems

Previous chapters have been written assuming the reader is writing standalone software – software which runs in what is called a freestanding environment in the C Standard – which does not require an operating system to run. While a great deal of embedded software falls into this category, it is worth briefly looking at software which is not expected to run in this way but instead requires what the C Standard refers to as a hosted environment. An operating system provides software and hardware management functions, such as task scheduling, IO control and memory management. Embedded operating systems are generally lightweight in comparison to the more familiar ones found on PCs, servers and other general-purpose computers; their design also often prioritises efficiency and determinism over extensive functionality and maintainability. ¹ A Real-time Operating System (RTOS) is one which has predictable task timing and is therefore well suited to time-critical applications.

Although having an operating system takes embedded programming a step closer to more general-purpose programming, it is still important to continue following the rules for writing good embedded software – a good operating system will give you some protection against some common programming errors, but it is still preferable to write good software rather than relying on the environment helping it to recover when an error does occur.
