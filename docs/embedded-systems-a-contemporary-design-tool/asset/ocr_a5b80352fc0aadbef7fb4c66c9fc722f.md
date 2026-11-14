# 11.15 THOUGHT QUESTIONS

# Programs and Processes

11.1 Can an embedded application have more than one process? If so, give several examples when one might want to design such a system. Discuss the advantages and disadvantages of such a design.

11.2 The chapter identified three general scheduling strategies. What are these examples, and what are their differences?

11.3 Give several examples of embedded applications when each of the scheduling strategies identified in question 11.2 might be used. Give several pros and cons for the choice of strategy for each application.

# Threads

11.4 Can a task or process have more than one thread? If so, what is the advantage of such a design? Are there disadvantages?

11.5 When should we use a heavyweight thread? a lightweight thread?

# Sharing Resources

11.6 Why is the supervisor mode necessary? When is it necessary? Under such circumstances, identify and elaborate on several problems that might occur if it is not used.

11.7 Are there embedded applications when the supervisor mode is not necessary? If so, give several examples and discuss why it is not necessary.

11.8 Why is it good practice to ensure that all functions are reentrant?

11.9 Give several examples of functions that are not reentrant.

# Foreground/Background Systems

11.10 What kinds of embedded designs are best suited for implementation using a foreground/background model?

# Kernels and Operating Systems

11.11 Discuss possible strengths and weaknesses of the architectural style used in most contemporary operating systems.

11.12 Identify some way in which an embedded operating system might be different from the one in your desktop computer? In what ways might they be the same?

11.13 When might one elect to use a foreground/background model in an embedded design? a basic kernel? a full-featured operating system?

11.14 Give several examples of when it would be necessary to incorporate real-time capabilities into the strategies discussed in Question 11.11.

# Interrupts

11.15 Give several examples of where an interrupt mask might be used.

11.16 What is interrupt priority? Why is it used? What determines the priority of an interrupt?

# Changing Contexts

11.17 Identify several cases when a context switch might be necessary in an embedded application.

11.18 Identify several events internal to an embedded system that might cause a context switch. Identify several events external to the system that might cause a context switch.

11.19 Identify and describe each of the major steps in a context switch when duplicate hardware is available; in a design using task control blocks; when a stack is used; in a foreground/background system.

11.20 Give several examples of embedded applications when each of the different kinds of stack discussed in this chapter might be used. Identify several pros and cons for your choice of stack in each application.

# 11.16 PROBLEMS

11.1 Give an example of an embedded application that has at least three tasks that run concurrently. Give a UML activity diagram expressing the behavior of these tasks.

11.2 Give a sequence diagram illustrating the context switch between the tasks in the system designed in Problem 11.16.1.

11.3 Give a UML class diagram for the single process illustrated in Figure 11.2.

11.4 If an embedded system has five processes with the following execution times, propose a schedule in which the average waiting time is the smallest: P1(9), P2(25), P3(4), P4(48), P5(12). Illustrate the scheduling using UML sequence diagram.

11.5 Present a UML activity diagram to illustrate the behavior of tasks in each of the following operating systems.