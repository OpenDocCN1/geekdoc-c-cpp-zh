the 14th and 15th registers appear as registers E and F in context 0 and as registers 0 and 1 in context 1. Using such a scheme, variables can easily be passed between contexts with no overhead.

# 11.12.2 Task Control Blocks

When a system is implemented using the TCB model, each TCB will contain all relevant information about the state of the task. To affect the context switch, necessary task state information is copied to the TCB. The TCB can then be inserted into the appropriate queue and the status and state information for the new or resumed task can be entered into the system variables. If the running task has been preempted, the TCB will be linked into the ready queue waiting for the CPU to become available. Based on the scheduling algorithm, it may or may not be the next task to run. If the task has blocked, the TCB will be linked into the waiting queue for the required resource. When the resource becomes available, the task will move to the ready queue.

# 11.12.3 Stacks

The stack is a rather simple data structure used for storing information associated with a task or thread. It is an area set aside in memory as part of system allocation. The information is held in a data structure similar to TCB called a stack frame or activation record. Typical information that must be stored is illustrated in Figure 11.21.

![](bbox=[0.28, 0.47, 0.85, 0.77])

When a stack is used, procedures must be written to manage the processes of saving, accessing, and removing information to or from the stack. Such procedures are initially invoked as part of a function call or by the interrupt handler prior to a context switch.