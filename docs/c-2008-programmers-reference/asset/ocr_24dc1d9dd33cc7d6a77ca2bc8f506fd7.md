Figure 10-4 shows graphically the two different threads of execution.

![](bbox=[0.22, 0.2, 0.92, 0.38])

Figure 10-4

# Passing Parameters to Threads

In the past few examples, you've seen how to create a thread using the ThreadStart delegate to point to a method. So far, though, the method that you have been pointing to does not have any parameters:

```
```csharp
static void DoSomething()
{
    ...
    ...
}
```
```

What if the function you want to invoke as a thread has a parameter? In that case, you have two choices:

+   - Wrap the function inside a class, and pass in the parameter via a property.
+   - Use the ParameterizedThreadStart delegate instead of the ThreadStart delegate.

Using the same example, the first choice is to wrap the DoSomething() method as a class and then expose a property to take in the parameter value:

```
```csharp
class Program
{
    static void Main(string[] args)
    {
        SomeClass sc = new SomeClass();
        sc.msg = "useful";
        Thread t = new Thread(new ThreadStart(sc.DoSomething));
        t.Start();
    }
}

class SomeClass
```