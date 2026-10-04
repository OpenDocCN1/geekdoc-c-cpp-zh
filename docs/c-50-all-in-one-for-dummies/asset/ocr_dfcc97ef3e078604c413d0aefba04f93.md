where the exception was thrown and how the program got there. Using that information, you should be drawn to the culprit like a tornado to a trailer park.

If you run the previous example and examine the stack trace it prints to the console, you see Main() at the bottom of the listing and deeper methods above it. The trace builds upward from Main(), so, technically, unwinding the call stack goes down the trace toward Main(). You should think of it the other way around, though: Callers are higher in the call chain (refer to Figure 9-1).

Returning geeky information such as the stack trace works just fine during development, but you would probably want real users to see more intelligible information. Still, you may want to write the stack trace to a log file somewhere.

The versions of Factorial() that I describe earlier in this chapter use a nonrecursive algorithm, which uses a loop to calculate the factorial. For a recursive version, see the RecursiveFactorial example on the web. A recursive method calls itself, possibly repeatedly until a stopping condition occurs. The recursive Factorial() calls itself repeatedly (recurses), stopping when the value that’s passed in becomes negative. Recursion is the most common way to implement Factorial(). Caution: Make sure that the recursion will stop. You can compare the results of RecursiveFactorial with those of the less exotic NonrecursiveFactorial example, and the DeadlyRecursion example shows what happens if the recursion doesn’t stop — it results in quite an unpleasant StackOverflowException.

While the program is running in the debugger, the stack trace is available in one of the Visual Studio debugger windows.

# Assigning Multiple catch Blocks

We mention earlier in this chapter that you can define your own custom exception types. Suppose that you defined a CustomException class. (We describe this process in the article “Creating Your Own Exception Class,” which you can find on http://csharp102.info.) Now consider the catch clause used here:

```
public void SomeMethod()
{
    try
    {
        SomeOtherMethod();
    }
    catch(CustomException ce)
    {
    }
}
```