# Thread Synchronization and Control Operations

When the user wants to close the application, we will open an event and set its state to signaled. In that way, the thread will exit on the next call to WaitForSingleObject. Then we will obtain the working thread identifier that is associated with the main window and wait for its exit using the WaitForSingleObject function.

# There's more...

We may conclude that if we set high priority for a thread, the application will execute faster. Well, this is incorrect. Pay attention that if you increase the priority for various applications (whether it is process or thread priority) the system will devote a lot of time for those threads, but it will not be able to perform its tasks, resulting in a slow or even unresponsive system. If you open the Task Manager, you will see only few windows/ processes are running on a higher priority than NORMAL. Usually those are dwm.exe (Desktop Window Manager) and taskmgr.exe (Windows Task Manager). Windows sets two desktop processes with higher priority to be able to respond to user commands, just like our application that prefers input over drawing (calculating). You must use priority with caution, and our advice is to increase priority only when you must.

# The Windows dispatcher object and scheduling

As we previously learned, in order to choose the next thread for execution, the dispatcher selects threads from the queue, starting from a higher priority to lower priority. The queue does not contain all the threads. Some of them are suspended or blocked. We previously said that there are three states: Running, Ready, and Blocked. These were basic condition states. Now, let's expand these states and explain them all.

At any instant, a thread can be in one of the following states:

+   - Ready: It resides in the queue waiting for execution
- Standby: It is next for execution
- Running: It is executing-it is waiting for a resume signal
- Transition: It is to be executed just soon as the system loads its context
- Terminated: It is done executing, but the object has not been deleted

When dispatcher selects the next thread for execution, the system loads its context into memory. The context contains a series of values such as machine register values, kernel stack, environment block, and user residing in the process address space, even though a part of the context was swapped to the disk, thread enters transition state, even though the system collects parts. Switching threads means saving all parts of the context and loading all parts of the next thread.