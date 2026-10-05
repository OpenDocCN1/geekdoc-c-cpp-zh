
will be allowed to load on such systems. All in, the reduction of third-party drivers that are allowed to load in kernel mode memory should result in significant stability and security improvements.

Certain vendors, platforms, and even enterprise configurations of Windows can have any number of these signing policies customized, such as through the Device Guard technology, which we will briefly describe in the upcoming "Hypervisor" section, and later in Chapter 7. As such, an enterprise might require WHQL signatures on Windows 10 client systems, or request the omission of this on a Windows Server 2016 system.

As you will see in Chapter 2, "System architecture," user applications switch from user mode to kernel mode when they make a service call. For example, a ReadFile function exists to call the internal routine that actually handles reading data from a file. That routine, because it accesses internal system data structures, must run in kernel mode. The use of a special instruction triggers the transition from user mode to kernel mode and causes the processor to enter the service dispatching code in the kernel. In turn this calls the appropriate internal function in Nkrnl.exe or Win32k.sys. Before returning control to the user thread, the processor is switched back to user mode. In this way, the OS protects itself and its data from processes.

> Note A transition from user mode to kernel mode (and back) does not affect thread scheduling per se. A transition is not a context switch. Further details on system dispatching are included in Chapter 2.

It’s normal for a user thread to spend time of its execution in user mode and part in kernel mode. In fact, the bulk of the graphics and windowing system also run in kernel mode, graphics-intensive applications spend more of their time in kernel mode than in user mode. An easy way to test this is to run a graphics-intensive application such as Microsoft Paint and paint the time split between user mode and kernel mode using one of the performance counters listed in Table 1-3. More advanced applications can use technologies such as Direct2D and DirectComposition, which perform computations in user mode and send only the raw surface data to the kernel. This reduces the time spent transitioning between user and kernel modes.

# TABLE 1-3 Mode-related performance counters

| Object: Counter | Function |
| :--- | :--- |
| Processor: % Privileged Time | Percentage of time that an individual CPU (or all CPUs) has run in kernel mode during a specified interval |
| Processor: % User Time | Percentage of time that an individual CPU (or all CPUs) has run in user mode during a specified interval |
| Process: % Privileged Time | Percentage of time that the threads in a process have run in kernel mode during a specified interval |
| Process: % User Time | Percentage of time that the threads in a process have run in user mode during a specified interval |
| Thread: % Privileged Time | Percentage of time that a thread has run in kernel mode during a specified interval |
| Thread: % User Time | Percentage of time that a thread has run in user mode during a specified interval |

CHAPTER 1 Concepts and tools 25

# EXPERIMENT Kernel mode vs. user mode

You can use the Performance Monitor to see how much time your system spends executing in kernel mode versus user mode. Follow these steps:

- 1. Open the Start menu and type Run Performance Monitor (it should be suggested before you typing) to run Performance Monitor.

- 2. Select the Performance Monitor node under Performance/Monitoring Tools in the tree on the left side.

- 3. To delete the default counter showing the total CPU time, click the Delete button on the toolbar or press the Suppr key on the keyboard.

- 4. Click the Add (+) button on the toolbar.

- 5. Expand the Processor counter section, click the % Privileged Time counter, and while holding down the Ctrl key, click the % User Time counter.

- 6. Click Add, and then click OK.

- 7. Open a command prompt and type dir \computername%s / to run a directory scan of your C drive.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_42_0.png)

- 8. When you're finished, close the toolbar.

You can also quickly see this by using Task Manager. Just click the Performance tab, right-click the CPU graph, and select Show Kernel Times. The CPU usage bar will show kernel-mode CPU time usage in a darker shade of light blue.

To see how the Performance Monitor uses kernel time and user time, run it again, add the individual process counters % User Time and % Privileged Time for every process in the system:

- 1. If it's not already running, running the Performance Monitor. (If it is already running, start with a blank display by right-clicking in the graph area and selecting Remove All Counters).
- 2. Click the Add button on the toolbar.
- 3. In the available counters, expand the Process section.
- 4. Select the % Privileged Time and % User Time counters.
- 5. Select a few processes in the Instance box (such as mmc, cssrs, and Idle).
- 6. Click Add, and then click Ok.
- 7. Move the mouse rapidly and forth.
- 8. Press Ctrl+H to turn on highlighting mode. This highlights the currently selected counter in black.
- 9. Scroll through the counters at the bottom of the display to identify the processes were running when you moved the mouse, and note whether they were running in user mode or kernel mode.

When you move the mouse, you should see the kernel-mode and user-mode time increase in the Instance column of mmc process in the Process Monitor. This is because the kernel handles the interrupts and the user-mode application then processes them. In this way, the OS protects itself and its data from processes.

> Note A transition from user mode to kernel mode (and back) does not affect thread scheduling per se. A transition is not a context switch. Further details on system dispatching are included in Chapter 2.

It’s normal for a user thread to spend time of its execution in user mode and part in kernel mode. In fact, the bulk of the graphics and windowing system also run in kernel mode, graphics-intensive applications spend more of their time in kernel mode than in user mode. An easy way to test this is to run a graphics-intensive application such as Microsoft Paint and paint the time split between user mode and kernel mode using one of the performance counters listed in Table 1-3. More advanced applications can use technologies such as Direct2D and DirectComposition, which perform computations in user mode and send only the raw surface data to the kernel. This reduces the time spent transitioning between user and kernel modes.
