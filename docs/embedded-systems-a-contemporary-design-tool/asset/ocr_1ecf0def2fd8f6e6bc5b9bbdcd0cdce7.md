# 11.13 SUMMARY

In this chapter we began the first portion of our study of tasks, threads, multitasking, the operating system, and the RTOS. We elaborated on the central responsibilities of an operating system, examined the characteristics and capabilities that distinguish an RTOS, and then identified the core set of requirements of the OS as embodied in the kernel. We then illustrated such capabilities through the design of several versions of a primitive

operating system kernel. We introduced some of the necessary terminology and examined the critical role of time in developing and deploying many embedded applications. Finally, we looked at different kinds of stacks and their role in managing context switches associated with task state changes, task preemption, or interrupts.

# 11.14 REVIEW QUESTIONS

# Programs and Processes

+   11.1 What is the difference between a program and a process?
+   11.2 What is the difference between a task and a process?
+   11.3 What is execution time? persistence?
+   11.4 Explain what is meant by task or process concurrency.
+   11.5 Why do we say that most of the time concurrent execution is only an illusion?
+   11.6 What is a process or task schedule? scheduling strategy?
+   11.7 Identify the major states in which a task or process within an embedded application might exist.

# Threads

+   11.8 What is a thread?
+   11.9 What is the difference between a task or process and a thread?
+   11.10 What is a lightweight thread? heavyweight thread?

# Sharing Resources

+   11.11 Identify several of the primary system resources that a task or process might require and use.
+   11.12 Identify several of the major responsibilities associated with managing the memory resource in an embedded design.
+   11.13 What is supervisor mode in a memory management scheme? User mode?
+   11.14 Identify several major responsibilities associated with process management.
+   11.15 What is reentrant code?

# Foreground/Background Systems

+   11.16 What is a foreground/background system?
+   11.17 What are some of the strengths of a foreground/background model?

+   11.18 What is the difference between a foreground and a background task?

# Kernels and Operating Systems

+   11.19 What is an operating system?
+   11.20 Identify and explain the core responsibilities of an operating system.
+   11.21 What are the major components of an operating system? Briefly describe the responsibilities of each component.
+   11.22 What is a real-time operating system?
+   11.23 What are some of the major characteristics that distinguish a real-time operating system from one that is not real time?
+   11.24 What is a task control block? What are some of the major components of a task control block?
+   11.25 What is an operating system kernel?
+   11.26 What is the difference between an operating system and an operating system kernel?

# Interrupts

+   11.27 What is an interrupt? Why is it used?
+   11.28 What is an interrupt number? What is its purpose?
+   11.29 What is an interrupt service routine? What is its purpose?
+   11.30 What is an interrupt vector table? What is its purpose?
+   11.31 Describe the sequence of steps that are necessary to handle an interrupt once one has occurred.
+   11.32 In the context of managing interrupts, what do the enable and disable commands do?
+   11.33 What is an interrupt mask? What is it used for?

# Changing Contexts

+   11.34 What is a context switch?
+   11.35 Identify several different kinds of stack that one might find in an embedded application.