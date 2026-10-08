# Can I Get an Exceptional Example? 195

The output from this program appears as follows (we trimmed the error messages to make them more readable):

```
i = 6, factorial = 720
i = 5, factorial = 120
i = 4, factorial = 24
i = 3, factorial = 6
i = 2, factorial = 2
i = 1, factorial = 1
Fatal error:
System.ArgumentException: Illegal negative argument to Factorial -1
at Factorial(Int32 value) in c:\programs\Program.cs:line 21
at FactorialException.Program.Main(String[] args) in c:\programs\nProgram.cs:line 49
Press Enter to terminate...
```

The first lines display the actual factorial of the numbers through 0. Attempting to calculate the factorial of -1 generates the message starting with Fatal error — that does not sound good.

The first line in the error message was formatted in Factorial() itself. This line describes the nature of the program, including the offending value -1.

# Tracing the stack

The remainder of the output is a stack trace. The first line of the stack trace describes where the exception was thrown. In this case, the exception was thrown in Factorial(int) — more specifically, Line 21 within the source file Program.cs.Factorial() was invoked in the Method Main(string()) on Line 50 within the same file. The stack trace stops with Main() because that's the module in which the exception was caught — end of stack trace.

You have to admit that this process is impressive — the message describes the problem and identifies the offending argument. The stack trace tells you where the exception was thrown and how the program got there. That information, you should be drawn to the problem like a tornado to a trailer park.

If you run the process again and examine the stack trace it prints to the console, you see Main() at the bottom of the list and deeper methods above it. The trace builds upward from Main(), so technically, unwinding the call stack goes down toward Main(). You should think of the other way around, though: Callers are higher in the chain (refer to Figure 9-1).

Returning geeky information such as the stack trace works fine during development, but you would probably want to see more intelligent information. Still, you might want to write the stack trace to a log file somewhere.