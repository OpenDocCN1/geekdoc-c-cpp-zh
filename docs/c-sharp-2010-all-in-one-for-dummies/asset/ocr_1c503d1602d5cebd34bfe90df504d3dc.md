The output from this program appears as follows (we trimmed the error messages to make them more readable):

```
```
i = 6, factorial = 720
i = 5, factorial = 120
i = 4, factorial = 24
i = 3, factorial = 6
i = 2, factorial = 2
i = 1, factorial = 1
i = 0, factorial = 0
Fatal error: System.ArgumentException: Illegal negative argument to Factorial -1
   at Factorial(Int32 value) in c:\programs\Factorial\Program.cs:line 21
   at FactorialException.Program.Main(String[] args) in c:\programs\Factorial\
Program.cs:line 49
Press Enter to terminate...
```
```

The first few lines display the actual factorial of the numbers 6 through 0. Attempting to calculate the factorial of –1 generates the message starting with Fatal error — that doesn’t sound good.

The first line in the error message was formatted back in Factorial() itself. This line describes the nature of the problem, including the offending value of –1.

# ## Tracing the stack

The remainder of the output is a stack trace. The first line of the stack trace describes where the exception was thrown. In this case, the exception was thrown in Factorial(int) — more specifically, Line 21 within the source file Program.cs. Factorial() was invoked in the method Main(string[] ) on Line 50 within the same file. The stack trace stops with Main() because that’s the module in which the exception was caught — end of stack trace.

You have to admit that this process is impressive — the message describes the problem and identifies the offending argument. The stack trace tells you where the exception was thrown and how the program got there. Using that information, you should be drawn to the problem like a tornado to a trailer park.

![](bbox=[0.067, 0.76, 0.123, 0.801])

If you run the previous example and examine the stack trace it prints to the console, you see Main() at the *bottom* of the listing and deeper methods above it. The trace builds upward from Main(), so, technically, unwinding the call stack goes *down* the trace toward Main(). You should think of it the other way around, though: Callers are higher in the call chain (refer to Figure 9-1).

![](bbox=[0.067, 0.859, 0.123, 0.899])

Returning geeky information such as the stack trace works just fine during development, but you would probably want real users to see more intelligible information. Still, you may want to write the stack trace to a log file somewhere.