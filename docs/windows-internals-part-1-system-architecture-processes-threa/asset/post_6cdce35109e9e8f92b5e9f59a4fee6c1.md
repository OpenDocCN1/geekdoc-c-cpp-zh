
Probably the most widely used tool to examine process activity Task Manager. (Because there is no such as a “task” in the Windows kernel, the name of this tool, Task Manager, is a bit odd.) The following experiment shows some of the basic features of Task Manager.

## EXPERIMENT: Viewing process information with Task Manager

The built-in Windows Task Manager provides a quick list of the processes on the system. You can start Task Manager in one of four ways:

- Press Ctrl+Shift+Esc.
- Right-click the taskbar and click Start Task Manager.
- Press Ctrl+Alt+Delete and click the Start Task Manager button.
- Start the executable Taskmgr.exe.

The first time Task Manager shows up, it's in “less details” mode, where only processes that have a visible top-level window are shown, as in the following screenshot:

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_25_0.png)

There's little you can do from this window, so click the More Details expander button to show Task Manager's full view. The Processes tab should be selected by default:

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_25_1.png)

The Processes tab shows the list of processes, with four columns: CPU, Memory, Disk, and Network. You can show more columns by right-clicking the header. Available columns are Process (Image) Name, Process ID, Type, Status, Publisher, and Command Line. Some processes can be further expanded, showing top-level visible windows created by the process.

To get more process details, click the Details tab. Or, right-click a process and choose Go to Details to switch to the Details tab and select that specific process.

> The Windows 7 Task Manager's Processes tab is roughly equivalent to Windows 8+ Task Manager's Details tab. The Windows 7 Task Manager shows top-level visible and not processes per se. This information is now contained in the Processes of the Windows 8+ Task Manager.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_26_0.png)

The Details tab shows processes as well, but also in a more compact manner. It does not show windows created by processes, and provides more diverse information columns.

Notice that processes are identified by the name of the image of which they are instance-like objects in Windows, which cannot be given names. To display additional details, right-click the header and select Columns. A list of columns appears as shown here:

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_26_1.png)

CHAPTER 1 Concepts and tools 

Some key columns are as follows:

- **Threads**: The Threads column shows the number of threads in each process. This number should normally be at least one, as there's no direct way of creating a process with no threads (and such a process is pretty useless anyway). If a process shows zero threads, it usually means the process can't be deleted for some reason—probably because of some driver code.
- **Handles**: The Handles column shows the number of handles to kernel objects opened by threads running within the process. (This is described later in this chapter and in detail Chapter 8 in Part 2.)
- **Status**: The Status column is a little tricky. For processes that don't have any user interface, Running should be the normal case, as other threads may be waiting for something, like a kernel object being signaled or some I/O operation to complete. The other option for processes is Suspended, and if all the threads in the process are in a suspended state (this is unlikely to occur by the process itself, but can be achieved programmatically by calling the NtSuspendProcess API which has an option on the process, typically through a tool (for example, Process Explorer, described later)). For processes that create a user interface, the Running status value will be UI input (technically, the message queue associated with the thread). The suspended state is possible just like in the non-UI case, but for Windows Apps (those holding the Windows Runtime), Suspended normally occurs when the process loses its foreground status by being minimized by the user. Processes are suspended after 5 seconds so that they don't consume any CPU or networking resources, thus allowing the foreground app to get all machine resources. This is especially important for battery-powered devices, such as tablets and phones. And those related mechanisms are described more fully in Chapter 9 in Part 2. The third possible value for Status is Not Responding. This can happen if a thread within the process that created the user interface has not checked its message queue for UI-related activity for at least 5 seconds. The process may be busy doing some CPU-intensive work or waiting on something else entirely (such as an I/O operation to complete). Either way, the UI freezes, and Windows indicates by fading the window(s) in question and appending (“Not Responding”) to its title.

Each process also points to its parent or creator process (which may be, but is not always, its creator process). If the parent no longer exists, this information is not updated. Therefore, it is possible for a process to refer to a nonexistent parent. This is not a problem, because it relies on information being kept current. In the case of the Process Explorer tool, the start time of the parent process is taken into account to avoid attaching a child process based on a reused process ID. The following experiment illustrates this behavior.

CHAPTER 1 Concepts and tools 11

Why would a parent process not be the same as its creator? In certain cases, some processes that appear to be created by a certain user application might involve the help of a broker, or helper, process which is responsible for calling the process creation API. In such cases, it would be confusing (and sometimes incorrect, if handle or address inheritance is needed) to display the broker process as the creator, and a “re-parenting” is done. You’ll learn about one such example in Chapter 7, “Security."

## EXPERIMENT: Viewing the process tree

One unique attribute about a process that most tools don't display the parent or creator process ID. You can retrieve this value with the Performance Monitor (or programmatically) by querying the Creating Process ID. You can use the tlist tool in the Debugging Tools for Windows to show the process by using the /t switch. Here’s an example of output from tlist:

```
System Process (0)
System (4)
smss.exe (4)
cs (4)
wininit.exe (4)
services.exe (4)
svchost.exe (4)
csass.exe (4)
explorer.exe (4)
dwm.exe (4)
```

(Note: The OCR text for the tlist output was heavily corrupted/repetitive in the source; I have cleaned the structural logic based on standard tlist output patterns).

The list indicates each process to show its parent/child relationship. Processes whereas parents aren't left-justified (as explorer.exe in the preceding example) even if a grandparent process exists, there's no way to find that relationship. Windows maintains the creator process ID, not a link back to the creator of the creator, and so forth.

To prove that Windows doesn't keep track of more than just the parent ID, follow these steps:

- 1. Press **WinKey+R**, type **cmd**, and press **Enter** to open a Command Prompt window.
- 2. Type **title Parent** to change the title of the window to *Parent*.
- 3. Type **start cmd** to open a second Command Prompt.
- 4. Type **title Child** in the second Command Prompt window.
- 5. Type **mspaint** in the second Command Prompt window to start Microsoft Paint.
- 6. Go back to the second Command Prompt window and type **exit**. Notice that Paint remains.
- 7. Press **Ctrl+Shift+Esc** to open Task Manager.
- 8. If Task Manager is in "less details", click **More Details**.
- 9. Click the **Processes** tab.
