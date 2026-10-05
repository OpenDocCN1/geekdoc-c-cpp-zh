The thread start address displayed might not be enough information to pinpoint what the thread is doing and which component within the process is responsible for the thread. This is especially true if the thread start address is a generic startup function—for example, if the function name does not indicate what the thread is actually doing. In this case, examining the thread might answer the question. To view the stack for a thread, double-click the thread of interest (or select it and click the Stack button). Process Explorer displays the thread's stack (both user and kernel, which was created in kernel).

> > Note While the user-mode debuggers (Winbg, Ntd, and Cdb) permit you to attach to a process and display the user stack for a thread, Process Explorer shows both the user and kernel stack in one easy click of a button. You can also examine user and kernel thread stacks using Winbg in local kernel debugging mode, as the next two experiments demonstrate.

When looking at 32-bit processes running on systems as 64-bit process (see Chapter 8 in Part 2 for more information on Wow64), Process Explorer shows both the 32-bit and 64-bit stack for threads. Because at the time of the real (64 bit) system call, the thread has been switched to a 64-bit stack and context, simply looking at the thread's 64-bit stack would reveal only half the story—the 64-bit part of the thread, with Wow64's thunk code. So, when examining Wow64 processes, be sure to take into account both the 32-bit and 64-bit stacks.

# EXPERIMENT: Viewing a thread stack with a user-mode debugger

Follow these steps to attach WinDbg to a process and view thread information and its stack:

+   1. Run notepad.exe and WinDbg.exe.
2. In WinDbg, open the File menu and select Attach to Process.
3. Find the notepad.exe instance and click OK to attach. The debugger should break into Notepad.
4. List the existing threads in the process with the ~ command. Each thread shows its debugger ID, client ID (ProcessID, ThreadID), its suspend count (this should be 1 most of the time, as it is suspended because of the breakpoint), the TB address, and whether it has been frozen using a debugger command.

```
0:005~
0 Id 612c.5f68 Suspend: 1 Teb: 0000002'41da2000 Unfrozen
1 Id 612c.5564 Suspend: 1 Teb: 0000002'41da4000 Unfrozen
2 Id 612c.4f88 Suspend: 1 Teb: 0000002'41da6000 Unfrozen
3 Id 612c.5608 Suspend: 1 Teb: 0000002'41da8000 Unfrozen
4 Id 612c.cf4 Suspend: 1 Teb: 0000002'41daa000 Unfrozen
5 Id 612c.9f8b Suspend: 1 Teb: 0000002'41db0000 Unfrozen
```