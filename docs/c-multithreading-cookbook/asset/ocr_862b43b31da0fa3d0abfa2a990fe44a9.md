In preemptive multitasking, the operating system collectively suspends thread execution, so that the other threads get equal processor time.

Obviously, preemptive multitasking has the ability to provide a much easier and safer task execution, with the fact that it does not depend on the processes' good or programmer's skill in handling over the control to the system.

# # Explaining the Windows Thread object

At the operating system level, a thread is an object created by the Object Manager. Like all the system objects, the thread has attributes (data) and methods (functions). The following table schematically shows the thread object and gives a list of its attributes and methods.

| Object attributes | Object methods |
|---|---|n| Client ID | Create thread |
| Context | Open thread |
| Dynamic priority | Query thread information |
| Base priority | Set thread information |
| Processor affinity | Current thread |
| Execution time | Terminate thread |
| Alert status | Get context |
| Suspension count | Set context |
| Impersonation symbol | Resume |
| Termination port | Alert |
| Exit status | Test alert |
| | Register termination port |

Most of the methods for threads have adequate Win32 API functions. For example, when we call SusThread, the Win32 subsystem calls the corresponding function. In other words, the Win32 API provides a method Sus for the Win32 applications.

Windows has always protected some internal structures, such as windows or brushes of direct manipulation. Threads that are executed on a user level cannot directly execute or modify the interior of the system object. It can only be done by calling the adequate Win32 API method that can do something with an object. Windows provides an identification code that identifies the object, while the programmers pass the identification code to the function that they need.