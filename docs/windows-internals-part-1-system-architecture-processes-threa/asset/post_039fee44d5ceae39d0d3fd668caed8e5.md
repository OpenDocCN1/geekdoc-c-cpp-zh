
# 10. Find the Command Processor app and expand its node. You should see the title Parent, in the following screenshot:

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_30_0.png)

11. Right-click the Windows Command Processor and select Go to details.

12. Right-click this cmd.exe process and select End Process Tree.

13. Click End Process Tree in the Task Manager confirmation dialog box.

The first Command Prompt will appear, but you should still see the Paint window because it was the grandchild of the command process you terminated. Because the intermediate process (parent of Paint) was terminated, there was no link between the parent and the grandchild.

Explorer, from Sysinternals, shows more details about processes and threads than any other available tool, which is why you will see it in a number of experiments throughout the book. Following are some of the unique things that Process Explorer shows enables:

- A process security token, as lists of groups and privileges and the virtualization store
- Highlighting to show changes in the process, thread, and handles list
- A list of services inside service-hosting processes, including the display name and description
- A list of additional process attributes, such as mitigation policies and their process protection level
- Processes that are part of a job and job details
- Processes hosting .NET applications and .NET-specific details, such as the list of AppDomains, loaded assemblies, and CLR performance counters
- Processes that host the Windows Runtime (immersion processes)
- The start time for processes and threads
- A complete list of memory-mapped files (not just DLLs)
- The ability to suspend a process or a thread
- The ability to kill an individual thread
- Easy identification of which processes were consuming the most CPU over a period of time

> **Note:** The Performance Monitor can display CPU utilization for a given set of processes, but it won't automatically show processes created after the performance-monitoring session has started. Only a manual trace in binary output format can do that.

Process Explorer also provides easy access to information in one place, such as the following:

- A process tree, with the ability to collapse parts of the tree
- Open handles in a process, including unnamed handles
- A list of DLLs (and memory-mapped files) in a process
- Thread activity within a process
- User-mode and kernel-mode thread stacks, including the mapping of addresses to names using the Dbghelp.dll that comes with the Debugging Tools for Windows
- More accurate CPU percentage using the thread cycle count—an even better representation of precise CPU activity, as explained in Chapter 4, “Threads."
- Integrity level
- Memory manager details such as peak commit charge and kernel memory paged and non-paged pool limits (other tools show only current size)

An introductory experiment using Process Explorer follows.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_31_0.png)

## EXPERIMENT: Viewing process details with Process Explorer

Download the latest version of Process Explorer from Sysinternals and run it. You can run it with standard user privileges. Alternatively, right-click the executable and select Run as Administrator to run it with administrator privileges. Running with admin privileges causes Process Explorer to install a driver that provides more features. The following description works the same regardless of how you launch Process Explorer.

The first time you run Process Explorer, you should configure symbols. If you don't, you will receive a message that symbols are not currently configured when you double-click a process and click the Threads tab. If properly configured, Process Explorer can access symbol information to display the symbolic name of the thread start function as well functions on thread's call stack. This is useful for identifying what threads are doing within process. To access symbols, you must have Debugging Tools for Windows installed (described later in this chapter). Then click Options, configure Symbols, and fill in the path to Dbghelp.dll in the Debugging Tools folder and valid symbol path. For example, on a 64-bit system, this configuration is correct if Debugging Tools for Windows are installed in the default location as of the WDK.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_32_0.png)

In the preceding example, the on-demand symbol server is used to access symbols and a copy of the symbol files is installed on the local machine in the C:\symbols folder. (You can replace this folder with some other folder, such as another drive, if free space is an). More information on configuring the use of the symbol server, see https://msdn.microsoft.com/en-us/library/windows/desktop/ee165fd8.aspx.

> **Tip:** You can configure the Microsoft symbol server by setting an environment variable named _NT_SYMBOL_PATH to the value shown in the graphic. Various tools use this variable automatically, as as Process Explorer, the debuggers that are part of the Debugging Tools for Windows, Visual Studio, and others. This will help you avoid having each tool separately.

When Process Explorer starts, it shows the process tree by default. You can expand the lower pane to display open handles or mapped DLLs and memory-mapped files. (These are explored in Chapter 5, "Memory management," and in Chapter 8 in Part 2.) It also shows a tooltip for the process command line and path, which becomes visible when you hover the mouse over the process name. For some types of processes, the tooltip also shows extra information, including the following:

- The services inside a service-hosting process (for example, svchost.exe)
- The tasks inside a task-hosting process (for example, TaskHost.exe)
- The target of a cmd-hosting process (also known as the default surrogate)
- The class information when hosted inside a dllhost.exe process
- The Provider for Windows Instrumentation (WMI) host processes such as WmiPrSE.exe (briefly discussed in "The Windows Runtime" section in this chapter)

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_33_0.png)

| Name | PID | CPU | Start Time | Private Bytes | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| services | 510 | 0 | 00:01 13:17:18-09 | 7,248 | 12,956 & Services Controller |
| svchost.exe | 512 | 0 | 00:01 13:17:18-06 | 4,488 | 54,485 & Service Group |
| svchost.exe | 514 | 0 | 00:01 13:14:05-09 | 38,100 | 83,290 & Shell Host |
| svchost.exe | 516 | 0 | 00:01 13:14:05-16 | 2,936 | 3,192 & LocalService Host |
| svchost.exe | 518 | 0 | 00:01 13:53:02-16 | 5,568 | 1,312 & RWorker |
| svchost.exe | 520 | 0 | 00:01 13:53:02-16 | 3,192 | 10,240 & LocalService Host |
| svchost.exe | 522 | 0 | 00:01 13:53:02-16 | 3,065 | 3,065 & LocalService Host |
| svchost.exe | 524 | 0 | 00:01 13:53:02-16 | 11,184 | 11,764 & LocalService Host |
| svchost.exe | 526 | 0 | 00:01 13:53:02-16 | 10,950 | 91,628 & LocalService Host |
| svchost.exe | 528 | 0 | 00:01 13:53:02-16 | 10,000 | 116,100 & LocalService Host |
| svchost.exe | 530 | 0 | 00:01 13:53:02-16 | 10,000 | 37,768 & Windows Session Manager |
| svchost.exe | 532 | 0 | 00:01 14:52:09-09 | 21,936 | 34,024 & Service Hosting Tool |
| svchost.exe | 534 | 0 | 00:01 13:21:03-16 | 13,024 | 25,424 & Service Subsystem App |
| svchost.exe | 536 | 0 | 00:01 13:21:03-16 | 13,024 | 13,608 & Runtime (UI) Host Shell Controller |
| svchost.exe | 538 | 0 | 00:01 15:56:04-16 | 6,456 | 23,998 & LocalService Host |
| svchost.exe | 540 | 0 | 00:01 13:53:02-16 | 13,024 | 23,996 & Host for Windows Services |
| svchost.exe | 542 | 0 | 00:01 13:53:02-16 | 226,754 | 264,620 & Host for Windows Services |
| svchost.exe | 544 | 0 | 00:01 13:53:02-16 | 226,108 | 344,000 & Host for Windows Services |
| svchost.exe | 546 | 0 | 00:01 13:53:02-16 | 10,972 | 10,972 & Host for Windows Services |
| svchost.exe | 548 | 0 | 00:01 13:53:02-16 | 10,972 | 10,972 & Host for Windows Services |
| svchost.exe | 550 | 0 | 00:01 13:53:02-16 | 3,298 | 3,298 & Host for Windows Services |
| svchost.exe | 552 | 0 | 00:01 13:53:02-16 | 20,452 | 36,296 & Host for Windows Services |
| svchost.exe | 554 | 0 | 00:01 13:53:02-16 | 4,508 | 11,548 & Host for Windows Services |
| svchost.exe | 556 | 0 | 00:01 13:53:02-16 | 7,876 | 7,876 & Host for Windows Services |
| svchost.exe | 558 | 0 | 00:01 13:53:02-16 | 21,528 | 21,528 & Host for Windows Services |
| svchost.exe | 560 | 0 | 00:01 13:53:02-16 | 17,768 | 38,244 & Host for Windows Services |
