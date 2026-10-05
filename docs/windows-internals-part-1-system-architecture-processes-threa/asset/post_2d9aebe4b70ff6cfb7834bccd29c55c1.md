
# Normal (Dynamic) Priorities
Real-Time Priorities

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_233_0.png)

FIGURE 4-7 A graphic view of thread priorities from a Windows API perspective.

TABLE 4-1 Mapping kernel priorities to the Windows API

| Priority Class Relative Priority | Real-Time | High | Above-Normal | Normal | Below-Normal | Idle |
|---|---|---|---|---|---|---|
| Critical (+Saturation) | 31 | 15 | 15 | 15 | 15 | 15 |
| Highest (+2) | 26 | 15 | 12 | 10 | 8 | 6 |
| Above Normal (+1) | 25 | 14 | 11 | 9 | 7 | 5 |
| Normal (0) | 24 | 13 | 10 | 8 | 6 | 4 |
| Below Normal (-1) | 23 | 12 | 9 | 7 | 5 | 3 |
| Lowest (-2) | 22 | 11 | 8 | 6 | 4 | 2 |
| Idle (-Saturation) | 16 | 1 | 1 | 1 | 1 | 1 |

You'll note that the Time-Critical and Idle thread priorities maintain their respective values regardless of the process priority class (unless it is Real-Time). This is because the Windows API requests saturation of the kernel, by passing in +16 or -16 as the requested relative priority. The formula used to get these values is (HIGH_PRIORITY equals 31):

If Time-Critical: ((HIGH_PRIORITY+1) / 2

If Idle: -((HIGH_PRIORITY+1) / 2)

These values are then recognized by the kernel as a request for saturation, and the Saturation field in KTHREAD is set. For positive saturation, this causes the thread to receive the highest possible priority within its priority class (dynamic or real-time); for negative saturation, it's the lowest possible one. Additionally, requests to change the base priority of the process will no longer affect the base priority of these threads because saturated threads are skipped in the processing code.

As shown in Table 4-1, threads have seven levels of possible priorities to set viewed from the Windows API for the High priority class. The Real-Time priority class allows setting all priority levels between 16 and 31 (as shown in Figure 4-7). The values not covered by the standard constants can be specified with the values -7, -6, -5, -4, -3, 4, 5, and 6 as an argument to SetThreadPriority. (See the upcoming section "Real-time priorities" for more information.)

Regardless of how the thread's priority comes to be using the Windows API (a combination of process class and a relative priority), from the point of view of the scheduler, only the final results matter. For example, priority level 10 can be obtained in two ways: a Normal priority process class (8) with a relative thread priority of Highest (+2), or an Above-Normal priority process class (10) and a Normal thread relative priority (0). From the scheduler's perspectives, these settings lead to the same value (10), these threads are identical in terms of their priority.

Whereas a process has a single base priority value, each thread has two priority values: current (dynamic) and base. Scheduling decisions are made on the current priority. As explained in the upcoming section "Priority boosts," under certain circumstances, the system increases the priority of threads in the dynamic range (1 through 15) for brief periods. Windows never adjusts the priority of threads in the Real-Time (16 through 31), they always have the same base and current priority.

A thread's initial base priority is inherited from the process priority. By default, it inherits its priority from current. You can change it using the Create-Process function or by the command-line start command. You can also change a process priority after it is created by using the SetPriorityClass function or by using various tools to that function, such as Task Manager or Process Explorer. (Right-click on the process and choose a new priority class.) For example, you can lower the priority of a CPU-intensive process so that it does not interfere with normal system activities. Changing the priority of a process changes the thread priorities up or down, but their relative priorities remain the same.

Normal, users applications and services start with a normal base priority, so their thread typically executes at priority level 8. However, some Windows processes (as the Session manager, Service Control Manager, and local security authentication process) have a base priority slightly higher than the default for the Normal class (8). This higher value ensures that the threads in these processes will all start at a higher priority than the default of 8.

# Real-Time priorities

You can raise or lower thread priorities within the dynamic range in any application. However, you must have the increasing scheduling privilege (SetIncreaseBasePriorityPrivilege) to enter the Real-Time range. Be aware that many Windows kernel-mode system threads run in the Real-Time priority range, so if threads spend excessive time running them, they could block system functions (such as in the memory manager, cache, or device drivers).

Using the standard Windows APIs, once a process has entered the Real-Time range, all its threads (Idle ones) run at one of the Real-Time priority levels. It is impossible to mix real-time and dynamic threads within the same process through standard interfaces. This is because the SetThreadPriority calls the native NtSetInformationThread API with the ThreadBasePriority information class, which allows priorities to remain only in the same range. Furthermore, this class allows priority changes only in the recognized Windows API deltas of–2 to 2 (or Time-Critical/Idle) unless the request comes from CSRSS or another real-time process. In others, this means that a real-time process can pick thread priorities anywhere between 16 and 31, even though the standard Windows API relative priorities would seem to limit its choices based on the table that was earlier.

As mentioned, calling SetThreadPriority with one of special values causes a call to NtSetInformationThread with the ThreadActualBasePriority information class, the kernel base priority for the thread can be set directly, in using a guaranteed range for real-time process.

> **Note** The real-time does not imply that Windows is a real-time OS in the common definition of the term. This is because Windows does not provide, real-time OS facilities, such as guaranteed interrupt latency or a way for threads to obtain a guaranteed execution time. The term *real-time* really just means "higher than all the others"

# Using tools to interact with priority

You can change (and view) the base-process priority with Task Manager and Process Explorer. You can kill individual threads in a process with Process Explorer (which should be done, of course, with extreme care).

You can view individual thread priorities with Performance Monitor, Process Explorer, or WinDbg. Although it might be useful to increase or decrease the priority of a process, it typically does not make sense to adjust thread priorities within a process because only a person who understands the program (in other words, the developer) would understand the relative importance of the threads within the process.

The only way to specify a starting priority class for a process is with the start command in the Windows command prompt. If you want to have a program start every time with a specific priority, you define a shortcut to use the start command by beginning the command with cmd /c. This command prompt executes the command on the command line, and terminates the command prompt. For example, to run Notepad in the Idle-process priority, the command is cmd /c start /low Notepad.exe.

# EXPERIMENT: Examining and specifying process and thread priorities

To examine and specify process and thread priorities, follow these steps:

- 1. Run Notepad normally—example, by typing **Notepad** in a command window.
- 2. Open Task Manager and click to the **Details** tab.
- 3. Add a column named **Base Priority**. This is the name Task Manager uses for priority class.
- 4. Find Notepad in the list. You should see something like the following:

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_236_0.png)

- 5. Notice the Notepad process with the Normal priority class (8) and Task Manager shows the Idle priority class as Low.
- 6. Open Process Explorer.
- 7. Double-click the Notepad process to show its Properties dialog box and click the Threads tab.
- 8. Select the first thread (if there's more than one). You should see something like this:

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_236_1.png)
