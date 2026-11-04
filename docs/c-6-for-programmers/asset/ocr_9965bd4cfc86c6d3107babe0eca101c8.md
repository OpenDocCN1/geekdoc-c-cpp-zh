you can include a catch block that does not specify an exception type—such a catch block (known as a general catch clause) catches all exception types. At least one catch block and/or a finally block (discussed in Section 13.5) must immediately follow a try block.

In Fig. 13.2, the first catch block catches FormatExceptions (thrown by method int.Parse), and the second catch block catches DivideByZeroExceptions (thrown by the CLR). If an exception occurs, the program executes only the first matching catch block. Both exception handlers in this example display an error-message dialog. After either catch block terminates, program control continues with the first statement after the last catch block (the end of the method, in this example). We'll soon take a deeper look at how the flow of control works in exception handling.

# 13.3.3 Uncaught Exceptions

An uncaught exception (or unhandled exception) is one for which there's no matching catch block. You saw the results of uncaught exceptions in the second and third outputs of Fig. 13.1. Recall that when exceptions occur in that example, the app terminates early (after displaying the exception's stack trace). The result of an uncaught exception depends on how you execute the program—Fig. 13.1 demonstrated the results of an uncaught exception when an app is executed using Debug > Start Without Debugging. If you run the app by using Debug > Start Debugging and the runtime environment detects an uncaught exception, the app pauses, and the Exception Assistant window (Fig. 13.3) appears.

![](bbox=[0.15, 0.72, 0.85, 0.9])

Fig. 13.3 | Exception Assistant.