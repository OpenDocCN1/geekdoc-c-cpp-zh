
# THE ABSTRACTION: THE PROCESS

ASIDE: DATA STRUCTURE — THE PROCESS LIST
Operating systems are replete with various important data structures that we will discuss in these notes. The process list (also called the task list) is the first such structure. In any OS that has the ability to run multiple processes at once will have something akin to this in order to keep track of all the running programs in the system. Sometimes people refer to the individual structure that stores information about a process as a Process Control Block (PCB), a fancy way of talking about a C structure that contains information about each process (sometimes called a process descriptor).

It has not yet cleaned up by (in UNIX-based systems, this is called the zombie state!). This final state can be useful as it allows other processes (usually the parent that created the process) to examine the return code of the process and see if the just-finished process executed successfully (usually, programs return zero in UNIX-based systems when they have accomplished a task successfully, and non-zero otherwise). When finished, the parent will make one final call (e.g., wait()) to wait for the completion of the child, and to also indicate to the OS that it can clean up any data structures referred to the non-extinct process.

# 4.6 Summary

We have introduced the most basic abstraction of the OS: the process. It is quite simply viewed as a running program. With this conceptual view in mind, we will move on to the n-gritty; the low-level mechanisms needed to implement processes, and the higher-level policies required to schedule them in an intelligent way. By combining mechanisms and policies, we will build up our understanding of how an operating system virtualizes the CPU.

> Yes, the zombie state. Just like real zombies, these zombies are relatively easy to kill. Different techniques are usually recommended.

# ASIDE: KEY PROCESS TERMS

- The **process** is the major OS abstraction of a running program. At any point in time, the process can be described by its state: the contents of memory in its **address space**, the contents of CPU registers (including the **program counter** and **stack pointer**, among others), and information about I/O (such as open files which can be read or written).

- The **process** API consists of calls programs can make related to processes. Typically, this includes creation, destruction, and other useful calls.

- Processes exist in one of many different **process states**, including running, ready to run, and blocked. Different events (e.g., getting scheduled or rescheduled, waiting for an I/O to complete) transition a process from one of these states to the other.

- A **process** list contains information about all processes in the system. Each entry is found in what is sometimes called a **process control block (PCB)**, which is really just a structure that contains information about a specific process.

# THE ABSTRACTION: THE PROCESS

37

# References

[H79] "The Nucleus of a Multiprogramming System" by Per Brinch Hansen, Communications of the ACM, Volume 134, April 1970. This paper introduces one of the first microkernels in operating systems, called Nucleus. The idea of smaller, more minimal systems is a theme that reads repeatedly in OS history; it all began with Brinch Hansen's work described herein. Nickolai

[Ck-08] "the xv6 Operating System" by Russ Cox, Frans Kaashek, Robert Morris, Nikolai Zeldovich. Download and play with it to learn more about the details of how operating systems actually work. From https://github.com/mit-pdos/xv6-public. The real and little OS in the world. It has been built using an older version (2012-01-30T2341432) and hence some examples in the book may not match the latest in the sources.

[DV66] "Programming Semantics for Multiprogramming Computations" by Jack B. Dennis, Earl C. Van Horn. Communications of the ACM, Volume 9, Number 3, March 1966. This paper defined many of the early terms and around building multiprogramming systems.

[L75] "Policy/mechanism separation in Hydra" by J. Levin, E. Cohen, R. Corvin, F. Pollack, W. Wald, Austin, November 1975. An early paper about how to structure operating systems in a research OS known as Hydra. Hydra never became a mainstream OS, some of its ideas influenced OS designers.

[V+65] "Structure of the Multics Supervisor" by I.A. Vyssotsky, F. J. Corbato, R. M. Graham. Fall Joint Computer Conference, 1965. An early paper on Multics, which described many of the basic ideas and terms that we find in modern systems. Some of the vision behind computing as a utility are finally realized in modern cloud systems.

# Homework (Simulation)

This program, process-run.py, allows you to see how process states change as programs run and either use the CPU (e.g., perform an add instruction) or do I/O (e.g., send a request to a disk and wait for it to complete). Use the README for details.

# Questions

- 1. Run process-run.py with the following flags: -l 5:100,5:100. What should the CPU utilization (e.g., the percent of time the CPU is in use?) Why do you know this? Use the -c and -p flags to see if you were right.

- 2. Now run with these flags: ./process-run.py -l 1:0,1:0. These flags specify one process with 4 instructions (all to use the CPU), and one simply issues an I/O and waits for it to be done. How long does it take to complete both processes? Use -c and -p to find out if you were right.

- 3. Switch the order of processes: -1 1:0,4:100. What happens now? Does switching the order matter? Why? (Always, use -c and -p to see if you were right)

- 4. We'll now explore some the other flags. One important flag is -S, which determines how the system reacts when a process issues an I/O. With the flag set to SWITCH_ON.END, the system will NOT switch to another process while is doing I/O, waiting until the process is completely finished. What happens when you run the following two processes (-1 1:0;4:100 -c SWITCH_ON.END), one doing I/O and the other doing CPU work?

- 5. Now, run the same processes, but with the switching behavior set to switch to another whenever is doing I/O. (-1 1:0;4:100 -c SWITCH_ON.END)

- 6. Other important behavior is what to do when an I/O completes. With the flag set to SWITCH_ON.END, the system will NOT switch to another process while is doing I/O, waiting until the process is completely finished. What happens when you run the following two processes (-1 1:0;4:100 -c SWITCH_ON.END), one doing I/O and the other doing CPU work?

- 7. Now, run the same processes, but with the switching behavior set to switch to another whenever is doing I/O. (-1 1:0;4:100 -c SWITCH_ON.END)

- 8. Now run with some randomly generated processes: -s 1 -1 3:50,3:50 or -s 2 -1 3:50,3:50 or -s 3 -1 3:50,3:50. See if you can predict how the trace will turn out. What happens when you use the flag -I RUN_IMMEDIATE vs. -I RUN_LATER? What happens when you use -S SWITCH_ON vs. -S SWITCH_END?
