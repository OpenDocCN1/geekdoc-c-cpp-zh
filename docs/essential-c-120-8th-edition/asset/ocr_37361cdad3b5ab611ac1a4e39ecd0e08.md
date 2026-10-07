# Chapter 8: Interfaces

Now consider a fully implemented version of this scenario with the following encapsulation requirements:

+   - It should not be possible to override Run().
- It should not be possible to invoke Start() or Stop(), as the order in which they execute is entirely under the control of the containing type (which we call IWorkflowActivity).
- It should be possible to replace whatever executes in the “Do something ...” code block.
- If it were reasonable to override Start() and Stop(), then the class implementing them should not necessarily be able to invoke them—they are part of the base implementation.
- The deriving types should be allowed to provide a Run() method, but it should not be invoked when the Run() method is invoked on IWorkflowActivity.

To meet all these requirements and more, C# 8.0 provides support for a protected interface member, which has some significant differences from a protected member on a class. Listing 8.14 demonstrates the differences, and Output 8.3 shows the results.

# Listing 8.14: Forcing the Desirable Run() Encapsulation

```
public interface IWorkflowActivity
{
    // Private and, therefore, not virtual
    private static void Start() =>
        Console.WriteLine("IWorkflowActivity.Start()...");

    // Sealed to prevent overriding.
    sealed void Run()
    {
        try
        {
            Start();
            InternalRun();
        }
        finally
        {
            Stop();
        }
    }
```