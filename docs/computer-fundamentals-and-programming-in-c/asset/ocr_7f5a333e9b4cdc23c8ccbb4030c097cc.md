# 5.7 TYPES OF OPERATING SYSTEMS

Modern computer operating systems may be classified into three groups according to the nature of interaction that takes place between the computer user and user’s program during its processing. The three groups are called batch process, time-shared, and real-time operating systems.

# 5.7.1 Batch Process Operating System

In a batch process operating system, environment users submit jobs to a central place where these jobs are collected in batch, and subsequently placed in an input queue in the computer where they are run. In this case, the user has no interaction with the job during its processing, and the computer’s response time is the turnaround time, that is, the time from submission of the job until execution is complete and the results are ready for return to the person who submitted the job.

A batch processing environment requires grouping of similar jobs that consist of programs, data, and system commands. When batch systems were first developed, they were defined by the ‘batching’ together of similar jobs. Card- and tape-based systems allowed only sequential access to programs and data, so only one application package (for instance, the FORTRAN compiler, linker, and loader, or the COBOL equivalents) could be used at a time. As online disk storage became feasible, it was possible to provide immediate access to all the application packages. Modern batch systems are no longer defined by the batching together similar jobs; other characteristics are used instead.

A batch operating system normally reads a stream of separate jobs (for example, from a card reader), each with its own control cards that predefine what the job does. When the job is complete, its output is usually printed (for example, on a line printer). The definitive feature of a batch system is the lack of interaction between the user and the job while the job is being executed. The job is prepared and submitted. The output appears later (perhaps after minutes, hours, or days). The delay between job submission and job completion, called the turnaround time, may result from the amount of computing needed or from delays before the operating system starts processing the job.

Process scheduling, i.e., allocation strategy for a process to a processor, memory management, file management, and I/O management in batch processing are quite simple. Jobs are typically processed in the order of submission, that is, on a first-come-first-serve basis.

A batch operating system generally manages the main memory by dividing it into two areas. One of them is permanently fixed for containing operating system routines and the other part contains only user programs to be executed; when one program is over, the next program is loaded into the same area. Since there is only one program in execution at a time, there is no competition for I/O devices. Therefore, allocation and de-allocation for I/O devices is very trivial. Access to files is also serial and there is hardly a need for protection and file access control mechanism.

This type of processing is suitable in programs with large computation time, with no need of user interaction or involvement. Some examples of such programs include payroll, forecasting, statistical analysis, and large, scientific, number-crunching programs. Users are not required to wait while the job is being processed. They can submit their programs to operators and return later to collect them.

A batch operating system has two major disadvantages and they are as follows.

**Non-interactive environment**  There are some difficulties with a batch system from the point of view of a programmer or user. Batch operating systems allow little or no interaction between users and executing programs. The turnaround time is very high. Users have no control over the intermediate results of a program. This type of arrangement does not provide any flexibility in software development.

**Offline debugging**  A programmer cannot correct bugs the moment they occur. Bugs are detected during program execution but are removed when not in execution.

# 5.7.2 Multiprogramming Operating System

A multiprogramming operating system allows more than one active user program (or part of user program) to be stored in the main memory simultaneously. Compared to batch operating systems, multiprogramming operating systems are fairly sophisticated. To have several jobs ready to run, the system must keep all of them in memory simultaneously. Having several programs in memory at the same time requires some form of memory management. In addition, if several jobs are ready to run at the same time, the system must choose the order in which each job has to be selected and executed one after the other. This decision is called CPU scheduling. Finally, multiple jobs running concurrently require that their ability to affect one another be limited in all phases of the operating system, including process scheduling, disk storage, and memory management.

Multiprogramming has significant potential for improving system throughput and resource utilization. Different forms of multiprogramming operating systems involve multitasking, multiprocessing, multi-user, or multi-access techniques. The main features and functions of such systems are discussed here briefly.

# Multitasking operating systems

A program in execution is called a process or task. A multiprogramming operating system is one, which in addition to supporting multiple concurrent processes, several processes in execution states simultaneously, allows the instruction and