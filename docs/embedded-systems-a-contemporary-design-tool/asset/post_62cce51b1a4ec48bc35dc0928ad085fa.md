
## 11.15 THOUGHT QUESTIONS

### Programs and Processes

11.1 Can an embedded application have more than one process? If so, give several examples when one might want to design such a system. Discuss the advantages and disadvantages of such a design.

11.2 The chapter identified three general scheduling strategies. What are these examples, and what are their differences?

11.3 Give several examples of embedded applications when each of the scheduling strategies identified in question 11.2 might be used. Give several pros and cons for the choice of strategy for each application.

### Threads

11.4 Can a task or process have more than one thread? If so, what is the advantage of such a design? Are there disadvantages?

11.5 When should we use a heavyweight thread? a lightweight thread?

### Sharing Resources

11.6 Why is the supervisor mode necessary? When is it necessary? Under such circumstances, identify and elaborate on several problems that might occur if it is not used.

11.7 Are there embedded applications when the supervisor mode is not necessary? If so, give several examples and discuss why it is not necessary.

11.8 Why is it good practice to ensure that all functions are reentrant?

11.9 Give several examples of functions that are not reentrant.

### Foreground/Background Systems

11.10 What kinds of embedded designs are best suited for implementation using a foreground/background model?

### Kernels and Operating Systems

11.11 Discuss possible strengths and weaknesses of the architectural style used in most contemporary operating systems.

11.12 Identify some way in which an embedded operating system might be different from the one in your desktop computer? In what ways might they be the same?

11.13 When might one elect to use a foreground/background model in an embedded design? a basic kernel? a full-featured operating system?

11.14 Give several examples of when it would be necessary to incorporate real-time capabilities into the strategies discussed in Question 11.11.

### Interrupts

11.15 Give several examples of where an interrupt mask might be used.

11.16 What is interrupt priority? Why is it used? What determines the priority of an interrupt?

### Changing Contexts

11.17 Identify several cases when a context switch might be necessary in an embedded application.

11.18 Identify several events internal to an embedded system that might cause a context switch. Identify several events external to the system that might cause a context switch.

11.19 Identify and describe each of the major steps in a context switch when duplicate hardware is available; in a design using task control blocks; when a stack is used; in a foreground/background system.

11.20 Give several examples of embedded applications when each of the different kinds of stack discussed in this chapter might be used. Identify several pros and cons for your choice of stack in each application.

## 11.16 PROBLEMS

11.1 Give an example of an embedded application that has at least three tasks that run concurrently. Give a UML activity diagram expressing the behavior of these tasks.

11.2 Give a sequence diagram illustrating the context switch between the tasks in the system designed in Problem 11.16.1.

11.3 Give a UML class diagram for the single process illustrated in Figure 11.2.

11.4 If an embedded system has five processes with the following execution times, propose a schedule in which the average waiting time is the smallest: P1(9), P2(25), P3(4), P4(48), P5(12). Illustrate the scheduling using UML sequence diagram.

11.5 Present a UML activity diagram to illustrate the behavior of tasks in each of the following operating systems.

(a) Single process–single thread
(b) Multiple process–single thread
(c) Single process–multiple threads
(d) Multiple process–multiple threads

For each case, identify which resources each process or thread is using.

11.6 Give an example of a function that is not reentrant. Give an example of a function that is reentrant. How would you modify your first function to make it reentrant?

11.7 Consider implementing an embedded system to control a traffic light as a foreground/background system. Each direction supports a left turn (right turn if traffic normally drives on the left hand side) and pedestrian-activated crosswalk control.

(a) Which tasks are foreground tasks?
(b) Which tasks are background tasks?
(c) Give a UML state diagram illustrating the behavior of the system during a change from north–south green to east–west green. Be certain to consider the operation of and without a left (right) turn and with and without a pedestrian.
(d) Give a UML sequence diagram for the events in part (c).

11.8 Repeat Problem 11.7 for a microwave cooker.

11.9 Repeat Problem 11.7 for a washing machine.

11.10 Repeat Problem 11.7 for a video-on-demand entertainment system for a large hotel.

11.11 Consider implementing an embedded system to control a traffic light as an RTOS-based system. Each direction supports a left turn (right turn if traffic normally drives on the left-hand side) and pedestrian-activated crosswalk control.

(a) Which tasks are the major tasks?
(b) Give a UML state diagram illustrating the behavior of the system during a change from north–south green to east–west green. Be certain to consider the operation of and without a left (right) turn and with and without a pedestrian.
(c) Give a UML sequence diagram for the events in part (c).

11.12 Repeat Problem 11.11 for a microwave cooker.

11.13 Repeat Problem 11.11 for a washing machine.

11.14 Repeat Problem 11.11 for a video-on-demand entertainment system for a large hotel.

11.15 Provide a UML class diagram for a task control block (TCB). Implement the design using a C struct data structure.

11.16 Design a method that would enable the dynamic allocation and deallocation of TCBs as tasks are created or terminated.

11.17 Modify the design in Example 11.2 to support a dynamic number of tasks in the task queue without using malloc and free (C) or new and delete (C++) while retaining the array as the queue container.

11.18 Provide a UML class diagram for a task queue that support the dynamic insertion and deletion of tasks.

11.19 Implement the task queue specified in Example 11.2 to use a doubly-linked list as the underlying data type for the queue container.

11.20 Combine the subsystems in Problem 11.16 and Problem 11.19.

11.21 Modify the design of the TCB in Problem 11.15 to support a task priority number in the range of {0–9}. Assume 0 is the highest and 9 the lowest priority.
Incorporate the modified TCB design into the task queue design in Problem 11.19. Modify the access method to always return the highest priority task.

11.22 Modify the design of the TCB in Problem 11.15 to support the inclusion of an estimate of execution time number in the range of {0–99}.
Incorporate the modified TCB design into the task queue design in Problem 11.19. Modify the access method to always return the shortest task.

11.23 Give a high-level description of how the system in Figure P11.1 works. You should not need more than 10 lines.

![](img/679b8d2d47f1bf86e17aca48f596f5cc_635_0.png)

11.24 Write a C program to implement the design given in the data/control flow diagram in Problem 11.23.

## Tasks and Task Management

## THINGS TO LOOK FOR ...

- The role of time in embedded designs.
- The definitions of reactive and time-based systems.
- The differences between preemptive and nonpreemptive systems.
- The need for effectively scheduling the use of the system CPU(s).
- The criteria for making scheduling decisions.
- Common scheduling algorithms.
- Real-time scheduling considerations.
- How scheduling algorithms might be evaluated.
- Methods for intertask communication.
- The critical section problem and several solutions.
- Methods for task synchronization.

## 12.1 INTRODUCTION

In the previous chapter we introduced some of the basic concepts and methods involved in controlling multitasking systems. We learned that foreground/background systems can be effective under real-time constraints and that the basic responsibilities of the operating system comprise task scheduling, intertask communication, and task dispatch. In addition, we introduced some of the issues associated with the context switch in preemptive systems.

In this chapter, we will examine the scheduling problem and intertask communication in greater detail. The resource management aspects of task scheduling and dispatch will be covered in the following chapter. We will go on by continuing the discussion of time and the critical role it plays in the design of embedded applications by introducing the concepts of reactive and time-based systems. We will present and discuss various metrics for specifying and assessing a task schedule. We will then investigate several different scheduling algorithms and analyze task synchronization and intertask communication in some detail. The focus will be primarily from the perspective of either a kernel-based or more complete operating system-based control strategy.
