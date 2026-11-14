To begin, an operating system must provide or support three specific functions.

+   1. Schedule task execution.
+   2. Dispatch a task to run.
+   3. Ensure communication and synchronization among tasks.

The scheduler determines which task will run and when it will do so. The dispatcher performs the necessary operations to start the task, and intertask or interprocess communication is the mechanism for exchanging data and information between tasks or processes on the same machine or on different ones. The kernel is the smallest portion of operating system that provides these functions.

+   scheduler, dispatcher
+   intertask or interprocess communication
+   kernel

In an embedded operating system, such functions are captured in the following types of services:

+   • **Process or Task Management**
+   The central component of task management entails the creation and deletion of user and system processes as well as the suspension and resumption of such processes. How the task management responsibilities are handled determines, in large part, whether the OS can be defined as real time. Additional responsibilities include the management of inter-process communication and of deadlocks. Deadlocks arise when two or more tasks need a resource that is held by some other task.

+   • **Memory Management**
+   Among other responsibilities, memory management services include the tracking and control of which tasks are loaded into memory, monitoring which parts of memory are being used and by whom, administering dynamic memory if it is used, and managing caching schemes.

+   • **I/O System Management**
+   Management of system input and output can include a wide range of responsibilities. An embedded application must interact with a great variety of different devices. In more complex systems, such interaction occurs through a special piece of software called a *device driver*. In a well-designed system, the internal side of that software has what is called a *common calling interface* – an application programmer’s interface (API). The motivation in such an approach is to permit the application software to interact with each of the different devices in the same way. With UNIX™, for example, everything looks like a file. The operating system must manage the interaction between each of those devices and the users or tasks in the application. Also included in such interaction is the caching and buffering of all input and output transactions as necessary.

+   device driver
+   common calling
+   interface, application
+   programmer's
+   interface API

+   • **File System Management**
+   As the name suggests, file system management responsibilities are directed toward the creation, deletion, and management of files and directories. Recall the discussions about file management problems with the Mars rover *Spirit*. In that instance, the directory structure could not be created during boot because of available memory limitations.

Another task that falls under the auspices of the file management portion of the OS is that of working with nonvolatile storage if such capability is included in the system. Duties can include routine backup of any data that is to be saved as well as emergency backup either as power is failing or as some other catastrophic event is occurring to the system.