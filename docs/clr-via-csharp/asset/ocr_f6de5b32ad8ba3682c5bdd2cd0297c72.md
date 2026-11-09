```
```csharp
using System;
using System.Threading;

public static class Program {
    public static void Main() {
        // Create a Timer object that knows to call our TimerCallback
        // method once every 2000 milliseconds.
        Timer t = new Timer(TimerCallback, null, 0, 2000);

        // Wait for the user to hit <Enter>
        Console.ReadLine();
    }

    private static void TimerCallback(Object o) {
        // Display the date/time when this method got called.
        Console.WriteLine("In TimerCallback: " + DateTime.Now);

        // Force a garbage collection to occur for this demo.
        GC.Collect();
    }
}
```
```

Compile this code from the command prompt without using any special compiler switches. When you run the resulting executable file, you'll see that the TimerCallback method is called just once!

From examining the code above, you'd think that the TimerCallback method would get called once every 2,000 milliseconds. After all, a Timer object is created, and the variable t refers to this object. As long as the timer object exists, the timer should keep firing. But you'll notice in the TimerCallback method that I force a garbage collection to occur by calling GC.Collect().

When the collection starts, it first assumes that all objects in the heap are unreachable (garbage); this includes the Timer object. Then, the collector examines the application's roots and sees that Main doesn't use the t variable after the initial assignment to it. Therefore, the application has no variable referring to the Timer object, and the garbage collection reclaims the memory for it; this stops the timer and explains why the TimerCallback method is called just once.

Let's say that you're using a debugger to step through Main, and a garbage collection just happens to occur just after t is assigned the address of the new Timer object. Then, let's say that you try to view the object that t refers to by using the debugger's Quick Watch window. What do you think will happen? The debugger can't show you the object because it was just garbage collected. This behavior would be considered very unexpected and undesirable by most developers, so Microsoft has come up with a solution.

When the JIT compiler compiles the IL for a method into native code, it checks to see if the assembly defining the method was compiled without optimizations and if the process is currently being executed under a debugger. If both are true, the JIT compiler generates the method's internal root table in such a way as to artificially extend the lifetime of all of the variables to the end of the method. In other words, the JIT compiler will trick itself into