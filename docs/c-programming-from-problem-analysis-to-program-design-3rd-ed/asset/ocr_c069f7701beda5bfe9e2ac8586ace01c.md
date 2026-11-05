![](bbox=[0.173, 0.095, 0.72, 0.287])

**Figure 12-12** Unhandled exception thrown—dividing by zero

Notice in Figure 12–12 that the line of the code where the error was found is highlighted in yellow.

The exact message from Figure 12–12 is also generated within a Windows application during run-time when an attempt to divide by zero is reached. The Windows application had a statement in a button event-handler method that tried to divide by zero. Like the console application that generated the messages for Figures 12–9 and 12–10, the divide by zero in the Windows application error was not detected during compilation; the exception was not thrown until the user selected the button wired to the event-handler method that included the division statement. If that button had never been clicked, the application would have run smoothly.

# Raising an Exception

If a program encounters an error such as division by zero during run-time, and the program cannot recover from the error, it **raises** or **throws an exception**. When this happens, execution halts in the current method and the common language runtime (CLR) attempts to locate an exception handler to handle the exception. An **exception handler** is a block of code that is executed when an exception occurs. You will learn how to write exception handlers in the next section.

If the CLR finds an exception handler in the current method, control is transferred to that code. If the current method does not contain an exception handler, that method is halted, and the parent method that called the method that threw the exception attempts to handle the exception. The exception is said to be **thrown back** to the calling method. If more than two methods are used, the exception continues to be thrown backward until it reaches the topmost method. If none of the methods includes code to handle the error, the CLR handles the exception—by halting the entire application. This can be very abrupt, as you saw with the messages displayed in Figures 12–9 through 12–12. Because data can be lost, you want to try to avoid such an experience with your programs. If the CLR handles the exception by halting your application, it is called an **unhandled exception**.