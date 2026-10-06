# Chapter 2

![](bbox=[0.342, 0.153, 0.657, 0.283])

Transition one sets the process in the blocked state for input. Transition two occurs when Scheduler picks another process for execution on the CPU. The third transition occurs when Scheduler picks this process, while the fourth transition occurs when the requested input becomes available.

# # Implementation of processes

In modern multitasking systems, the Process Control Block (PCB) stores many different items of data, all needed for correct and efficient process management. PCB is the data structure that resides in the operating system kernel which contains the information needed to manage the process. The PCB is the representation of the process in the operating system. Though the details of these structures are system-dependent, there are some common parts, which could be classified into three main categories:

+   * Process identification data
* Process state data
* Process control data

| pointer | process state |
|---|---|
| process number |
| instruction pointer |
| registers |
| memory limits |
| list of open files |
| ... |

51