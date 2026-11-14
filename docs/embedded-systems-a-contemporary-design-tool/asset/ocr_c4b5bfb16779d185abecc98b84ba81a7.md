can compute the third. Though useful for comparing algorithms, it has limitations. The mathematics of complex algorithms and distributions is difficult to work with. The arrival and service distributions are complex, and the queuing models are only an approximation of the real system.

# 12.6.3 Simulation

To produce a more accurate evaluation of a scheduling algorithm, one can use simulations. Such an approach requires models of the computer system and the processes as well as appropriate data to drive the simulation. Often such data is collected from a trace of actual processes by recording the actual events on a real system. Simulation can be expensive, but it is growing in popularity and is becoming an increasingly powerful and effective tool.

# 12.6.4 Implementation

As another alternative, one can simply build and test the system. Certainly, this is the most accurate method. Once again, the difficulty is the cost.

# 12.7 TASKS, THREADS, AND COMMUNICATION

# 12.7.1 Getting Started

A multitasking/multithreading system supports multiple tasks and those tasks will have one or more threads. Important jobs in any multitasking system include exchanging data between tasks and between threads, synchronizing tasks and threads, and sharing resources.

In the not too recent past, such activities were limited primarily to tasks or threads within a single microprocessor. Today, one finds a growing use of Field Programmable Gate Array (FPGA)-based designs utilizing devices that support the inclusion of multiple microprocessor cores within a single-gate array. Consequently, it is not uncommon for communication, synchronization, and sharing to involve tasks on multiple processors. We will find that certain assumptions can be made when tasks are localized that cannot be made when working with multiple distributed processors or other centers of computation.

# 12.7.2 Intertask / Interthread Communication

When tasks are operating independently, systems have few, if any, conflicts, chances for corruption, or contentions. Real systems, the interesting ones, must deal with the challenge of such problems. In real-world systems, resource sharing and intertask synchronization and communication must take place in a robust, safe, and reliable manner. Interaction between tasks may be direct or indirect and must be synchronized and coordinated. We want to prevent race conditions – conditions under which the outcome of a computation depends on the order in which tasks execute. Such an exchange is illustrated in Figure 12.9.

We see, then, that interaction and interchange among tasks requires three basic components: the information that is to be interchanged, the places where the information can be found, and where it is ultimately to be put, coupled with the conventions that govern the interaction and interchange. These requirements are captured in the following model of inter-process communication and synchronization.