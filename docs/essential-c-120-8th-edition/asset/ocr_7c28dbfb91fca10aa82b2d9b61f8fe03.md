# ADVANCED TOPIC

# Dealing with Unhandled Exceptions on a Thread

As we discussed earlier, an unhandled exception on any thread by default causes the application to shut down. An unhandled exception is a fatal, unexpected bug, and the exception may have occurred because a crucial data structure is corrupt. Since you have no idea what the program could possibly be doing, the safest thing to do is to shut down the whole thing immediately.

Ideally, no programs would throw unhandled exceptions on any thread; programs that do have bugs, and the best course of action is to find and fix the bug before the software is shipped to customers. However, rather than shutting down an application as soon as possible when an unhandled exception occurs, it is often desirable to save any working data andor log the exception for error reporting and future debugging. This requires a mechanism to register notifications of unhandled exceptions.

With both the Microsoft .NET Framework and .NET Core 2.0 (or later), every AppDomain provides such a mechanism, and to observe the unhandled exceptions that occur in an AppDomain, you must add a handler to the UnhandledException event. The UnhandledException event will fire for all unhandled exceptions on threads within the application domain, whether it is the main thread or a worker thread. Note that the purpose of this mechanism is notification; it does not permit the application to recover from the unhandled exception and continue executing. After the event handlers run, the application will display the operating system's error reporting dialog, and then the application will exit. (For console applications, the exception details will also appear on the console).

In Listing 19.7, we show how to create a second thread that throws an exception, which is then handled by the application domain's unhandled exception handler. For demonstration purposes, to ensure that threading issues do not come into play, we insert some artificial delays using Thread.Sleep. Output 19.4 shows the results.

# LISTING 19.7: Registering for Unhandled Exceptions

```
using System;
using System.Diagnostics;
using System.Threading;
```