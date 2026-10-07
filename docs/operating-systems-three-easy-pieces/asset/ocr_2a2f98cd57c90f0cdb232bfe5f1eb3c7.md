# Mechanism: Limited Direct Execution

In order to virtualize the CPU, the operating system needs to somehow share the physical CPU among many jobs seemingly running at the same time. The basic idea is simple: run one process for a little while, then run another one, and so forth. By time sharing the CPU in this manner, virtualization is achieved.

There are a few challenges, however, in building virtualization machinery. The first is performance: how can we implement virtualization without adding excessive overhead to the system? The second is control: how can we run processes efficiently while retaining control over the CPU? Control is particularly important to the OS, as it is in charge of resources; without control, a process could simply run forever and take over the machine, or access information that should not be allowed to access. Obtaining high performance while maintaining control is thus one of the central challenges in building an operating system.

> THE CRUX: How To Efficiently Virtualize The CPU With Control
The OS must virtualize the CPU in an efficient manner while retaining control over the system. To do so, both hardware and operating-system support will be required. The OS will often use a judicious bit of hardware-support to accomplish its work effectively.

# 6.1 Basic Technique: Limited Direct Execution

To make a program run fast as one might expect, not surprisingly OS developers can use a technique, which we can call limited direct execution. The "direct execution" part of the idea is simple: just run the program directly on the CPU. Thus, when the OS wishes to start a program running, it creates a process entry for it in a process list, allocates some memory for it, loads the program code into memory (from disk), allocates its entry point (i.e., the main() routine or something similar), jumps