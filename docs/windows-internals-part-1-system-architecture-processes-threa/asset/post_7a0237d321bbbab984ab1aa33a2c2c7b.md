
## EXPERIMENT Viewing protected process thread information with Process Explorer

In this experiment, you'll view protected process thread information. Follow these steps:

- 1. Find any protected or PPL process, such as the Audiodg.exe or csrss.exe.
- 2. Open the process's Properties dialog box and click the Threads tab.![](img/ff0e6a9d867a3a6e9527eb1d946810fc_229.png)
- 3. Process Explorer doesn't show the start address instead it displays the standard wrapper inside ntdll.dll. If you click Stack, you'll get an error because although base priorities are shown, dynamic priorities are not (THREAD_QUERY_INFORMATION).
- 4. Try to kill a thread. When you notice the lack of THREAD_TERMINATE.

## Thread scheduling

This section describes Windows scheduling policies and algorithms. The subsection provides a condensed description of how scheduling works on Windows and a definition of key terms. After a review of Windows utilities and tools that relate to scheduling, the detailed data structures and algorithms that make up the Windows scheduling system are presented, including a description of common scheduling scenarios and how thread selection occurs.

## Overview of Windows scheduling

Windows implements a priority-driven, preemptive scheduling system. At least one of the highest-priority runnable (ready) threads always runs, with the caveat that certain high-priority threads might be limited by the processors on which they are allowed to run. Processor affinity is defined based on the process group assigned to threads by default (this is to maintain compatibility with older versions of Windows which supported only one processor). Developers can alter processor affinity using the appropriate APIs or by setting an affinity mask in the process header. However, multiple threads in a process can be associated with different groups and theoretically run its threads on any available processor. Additionally, developers can choose to create group-aware applications which use extended scheduling APIs to associate threads on different groups with their affinity.

After a thread is selected to run, it runs for an amount of time called a quantum. A quantum is the length of time a thread is allowed to run before another thread at the same priority level is given a turn. Quantum values vary from system to process for three reasons:

- System configuration (long or short quantums, variable or fixed quantums, and priority separation)
- Foreground or background status of the process
- Use of job objects to alter the quantum

These details are explained in the “Quantum” section later in this chapter.

A thread might not get to complete its quantum however because Windows implements a preemptive scheduler. That is, if another thread with a higher priority becomes ready to run, the currently running thread might be preempted before its slice. In fact, a thread can be selected to run next and be preempted before beginning its quantum.

The Windows scheduling code is implemented in the kernel. There is no single "scheduler" module or runtime. The code is spread throughout the kernel in which scheduling-related events occur. The routines that perform these duties are collectively called the kernel's dispatcher. The following events might require thread dispatching:

- A thread becomes ready to execute—for example, a thread has been newly created or has just been released from the wait state. own- A thread leaves the running state because its time quantum ends, it terminates, it yields execution, or it enters a wait state.
- A thread's priority changes, either because of a system service call or because Windows itself changes the priority value.
- A thread's processor affinity changes so that it will no longer run on the processor on which it was running.

At each of these junctions, Windows must determine which thread should run on the logical processor applicable, or on which logical processor the thread should now run. After a logical processor has selected a new thread to run, it eventually performs a context switch to it. A context switch is the procedure of saving the volatile processor's state associated with a running thread, loading another thread's volatile state, and starting the new thread's execution.

As noted, Windows schedules at the thread granularity level. This approach makes sense when you consider that processes don't run; rather, they only provide resources and a context in which their threads run. Scheduling decisions are made strictly on a thread basis, no consideration is given what process the thread belongs to. For example, if process A has 10 runnable threads, process B has 2 threads, and all 12 are at the same priority, each thread would theoretically receive one-twelfth of the CPU time. That is, Windows wouldn't give 50 percent of the CPU to process A and 50 percent to process B.

## Priority levels

To understand the thread-scheduling algorithms, one must first understand the priority levels that Windows uses. As illustrated in Figure 4-6, Windows uses 32 priority levels internally, ranging from 0 to 31 (which is the highest). These values divide up as follows:

- Sixteen real-time levels (16 through 31)
- Sixteen variable levels (0 through 15), out of which level 0 is reserved for the idle thread (described in Chapter 5).![](img/ff0e6a9d867a3a6e9527eb1d946810fc_231.png)

FIGURE 4-6 Thread priority levels.

Thread priority levels assigned from two perspectives: those of the Windows API and those of the Windows kernel. The Windows API first organizes processes by the priority class to which they are assigned (the in parentheses represent the internal PROCESS_PRIORITY_CLASS recognized by the kernel):

- Real-Time (4)
- High (3)
- Above Normal (6)
- Normal (2)
- Below Normal (5)
- Idle (1)

The Windows API SetPriorityClass allows changing a process's priority class to one of these levels. It assigns a relative priority of the individual threads within those processes. Here, the numbers represent a priority delta that is applied to the base priority:

- Time-Critical (15)
- Highest (2)
- Above-Normal (1)
- Normal (0)
- Below-Normal (-1)
- Lowest (-2)
- Idle (-15)

Time-Critical and Idle levels (+15 and -15) are called saturation values and represent specific levels that are applied rather true offsets. These values can be passed to the SetThreadPriority API to change a thread's relative priority.

In the Windows API, each thread has a base priority that is a function of its process class and its relative priority. In the kernel, the process priority class is converted to a base priority by using the PspPriorityTable global array and the PROCESS_ORITY_CLASS indices show earlier, which sets priorities of 4, 8, 13, 14, 6, and 10, respectively. (This is a fixed mapping that cannot be changed.) The relative priority is then applied as a differential to this base priority. For example, a Highest thread will receive a base priority of two levels higher than the base priority of its process.
