Now if you run the application again with an invalid file path, you'll see the debugger break at the point the exception is thrown, as shown in Figure 8.11. That is, at the point where it starts to pop up in our own code because the real origin is deep in the stomach of the BCL code.

![](bbox=[0.06, 0.24, 0.83, 0.62])

FIGURE 8.11 A first-chance exception notification.

Notice the Call Stack window now that the Just My Code option is disabled. The exception was really thrown by some helper method called __Error.WinIOError in a response to initialization of a FileStream object through the use of a StreamReader. This illustrates where the exception starts its life and how it bubbles up the call stack to a point where it can get handled. Figure 8.12 shows a stack walk carried out by the runtime to find an exception handler.

![](bbox=[0.1, 0.78, 0.75, 0.94])

FIGURE 8.12 Walking the stack to find an appropriate handler.