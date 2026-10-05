You can also quickly see this by using Task Manager. Just click the Performance tab, right-click the CPU graph, and select Show Kernel Times. The CPU usage bar will show kernel-mode CPU time usage in a darker shade of light blue.

To see how the Performance Monitor uses kernel time and user time, run it again, add the individual process counters % User Time and % Privileged Time for every process in the system:

+   1. If it's not already running, running the Performance Monitor. (If it is already running, start with a blank display by right-clicking in the graph area and selecting Remove All Counters).
2. Click the Add button on the toolbar.
3. In the available counters, expand the Process section.
4. Select the % Privileged Time and % User Time counters.
5. Select a few processes in the Instance box (such as mmc, cssrs, and Idle).
6. Click Add, and then click Ok.
7. Move the mouse rapidly and forth.
8. Press Ctrl+H to turn on highlighting mode. This highlights the currently selected counter in black.
9. Scroll through the counters at the bottom of the display to identify the processes were running when you moved the mouse, and note whether they were running in user mode or kernel mode.

When you move the mouse, you should see the kernel-mode and user-mode time increase in the Instance column of mmc process in the Process Monitor. This is because the process is executing application code in user mode and calling Windows functions that run in kernel mode. You'll also notice kernel-mode thread activity in the process named cssrs when you move the mouse. This activity occurs because the Windows subsystem's kernel-mode raw input thread, which handles keyboard and mouse input, is attached to this process. (See Chapter 2 for more information about threads and subsystems.) Finally, the Idle process that you spend nearly 100 percent of its time in kernel mode isn't a process—it's a fake process used to account for idle CPU cycles. As you can observe from the mode in which the threads in the Idle process run, when Windows has nothing to do, it does in kernel mode.

# Hypervisor

Recent shifts in application and software models, such as the introduction of cloud-based services and the pervasiveness of IoT devices, have resulted in the need for operating systems and hardware vendors to figure out more efficient ways to virtualize other guests on the hardware of the machine.