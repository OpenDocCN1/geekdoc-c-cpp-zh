
Once complete, the heap contains some marked and at least one unmarked objects. The marked objects must survive the collection because there is a root that refers to the object; we say that the object is reachable because application code can reach (or access) the object by way of the variable that still refers to it. Unmarked objects are unreachable because there is no root existing in the application that would allow for the object to ever be accessed again.

![](img/0ce3b788d061e3d3095fa554b1a34adf_534_0.png)

Managed heap

![](img/0ce3b788d061e3d3095fa554b1a34adf_534_1.png)

NextObjPtr

**FIGURE 21-2** Managed heap before a collection.

Now that the CLR knows which objects must survive and which objects can be deleted, it begins the GC's compacting phase. During the compaction phase, the CLR shifts the memory consumed by the marked objects down in the heap, compacting all surviving objects together that they are contiguous in memory. This serves many benefits. First, all the surviving objects will be next to each other in memory; this restores locality of reference reducing your application's working set size, improving the performance of accessing these objects in the future. Second, the free space is contiguous as well, so this region of address space can be free, allowing other things to use it. Finally, compaction ensures that there is no space fragmentation issues with the managed heap as is known to have with native heaps¹

When compaction, the CLR is moving objects around memory. This is a problem because any root that referred to a surviving object now refers to where in memory; not where the object has been relocated. When the application's threads eventually get resumed, they would access the old memory locations and corrupt memory. Clearly, this can't be allowed and so, as part of the compaction phase, the CLR subtracts from each root the number of bytes that the object referred to was shifted down in memory. This ensures that every root refers to the same object it before; it's just that the object is at a different location in memory.

After the heap is compacted, the managed heap NextObjPtr is set to point to a location just after the last surviving object. This is where the next allocated object will be placed in memory. Figure 21-3 shows the managed heap after the compaction phase. After the operation is complete, the CLR resumes all the application's threads and they continue to access the objects as if the GC never happened at all.

> Objects in the large object heap (discussed in this chapter) do not get compacted, and therefore address fragmentation is possible with the large object heap.

![](img/0ce3b788d061e3d3095fa554b1a34adf_535_0.png)

**FIGURE 21-3** Managed heap after a collection.

If the CLR is unable to reclaim memory after a GC and if there is no address space left in the processes to allocate a new GC, then there is no memory available for this process. In this case, the new object that attempted to allocate more memory ends up throwing an OutMemoryException. Your application can catch and recover from it but most applications do not attempt to do so; instead, the exception becomes an unhandled exception, Windows terminates the process, and Windows reclaims all the memory that the process was using.

As a programmer, notice how the two bugs described at the beginning of this chapter no longer exist. First, it is not possible to leak any object not accessible from your application's roots will be collected at some point. Second, it is not possible to corrupt memory by accessing an object that was freed because references can only refer to living objects, this is what keeps the objects alive.

> **Important** A static field keeps whatever object it refers to forever or until the AppDomain that the types are loaded into is unloaded. A common way to leak memory is to have a static field refer to a collection object and then keep adding items to the collection object. The static field keeps the collection object alive and the collection object keeps all its items alive. For this reason, it is best to avoid static fields whenever possible.

# Garbage Collections and Debugging

As soon as a root goes out of scope, the object it refers to is unreachable and subject to having its memory reclaimed by a GC; objects are not guaranteed to live throughout a method's lifetime. This can have an interesting impact on your application. For example, examine the following code.

```c
using System;
using System.Threading;

public static class Program {
  public static void Main() {
    // Create a Timer object that knows to call our TimerCallback
    // method every 2000 milliseconds.
    Timer t = new Timer(TimerCallback, null, 0, 2000);

// Wait for the user to hit <Enter>.
    Console.ReadLine();
}

private static void TimerCallback(Object o) {
    // Display the date/time when this method got called.
    Console.WriteLine("In TimerCallback: " + DateTime.Now());

    // For a garbage collection to occur for this demo.
    GC.Collect();
}
}
```

Compile this code from the command prompt without using any special compiler switches. You'll see that the TimerCallback method is called only once when you run the resulting executable file,

Examining the preceding code, you'd think that the TimerCallback method would be called once every 2,000 milliseconds. After all, a timer is created, and the variable t refers to this object. As long as the timer exists, the timer should keep firing. But you'll notice in the TimerCallback method that I force a garbage collection by calling GC.Collect().

When the collection starts, it first assumes that all objects in the heap are unreachable (garbage); this includes the Timer object. The collector examines the application's roots and sees that Main doesn't use the t variable after the initial assignment to it. The application has no variable referring to the Timer object, and the garbage collection reclaims the memory for it; this stops the timer and explains why the TimerCallback method is called just once.

Let's say you're using a debugger to step through Main, and a garbage collection happens just after t is assigned the address of the new Timer object. Then, let's say you try to view the object that t refers to by using the debugger's Quick Watch. What do you see? The debugger can't show the object because it was garbage collected. This behavior would be considered very unexpected and undesirable by most developers, so Microsoft has come up with a solution.

When you compile your assembly using the C# switch, the compiler applies a System.Diagnostics.DebuggableAttribute[DisableOptimizations] flag set into the resulting assembly. At runtime, when compiling a method, the JIT compiler sees this flag, and artificially extends the lifetime of all roots to the end of the method. For example, the JIT compiler tricks itself into believing that the variable t in Main will live until the end of the method. So, if a garbage collection were to occur, the garbage collector now knows that t is still a root and that the Timer object t refers to will continue to be reachable. The Timer object will survive the collection, and the TimerCallback method will get called repeatedly until Console.ReadLine returns and exits.

To see this, debug the program from a command prompt, but by this time, the C# compiler's /debug switch. When you run the resulting executable file, you'll now see that the TimerCallback method is called repeatedly. Note, the C# compiler's /optimize switch turns optimizations back on, so this compiler switch should not be used when performing this experiment.

The JIT compiler does this to help you with JIT debugging. You may now start your application normally (without a debugger), and if the method is called, the JIT compiler will artificially extend the lifetime of the variables to the end of the method. It's ironic: by explicitly indicating where you want the timer to be disposed, it must remain alive up to that point.

So now know how to build a program that works in a debug build but doesn't work when you make a release build. Because no developer wants a program that only works when debugging, you could try modifying the Main method to do the following.

```c
public static void Main() {
    // Create a Timer object that knows to call our TimerCallback
    // method every 2000 milliseconds.
    Timer t = new Timer(TimerCallback, null, 0, 2000);

    // Wait for the user to hit <Enter>.
    Console.ReadLine();

    // Refer to t after Readline (this gets optimized away)
    t = null;
}
```

However, if you compile this (without the /debug+ switch) and run the resulting executable file, you'll see that the TimerCallback method is called once. The problem is that the JIT compiler is an optimizing compiler, and setting a local variable or parameter variable to null is the same as not referencing the variable at all. In other words, the JIT compiler optimizes the t = null; line out of code completely, and therefore, the program still does not work as we desire. The correct way to make the Main method is as follows.

```c
public static void Main() {
    // Create a Timer object that knows to call our TimerCallback
    // method every 2000 milliseconds.
    Timer t = new Timer(TimerCallback, null, 0, 2000);

    // Wait for the user to hit <Enter>.
    Console.ReadLine();

    // Refer to t after ReadLine (t will survive GCs until Dispose returns)
    t.Dispose();
}
```

Now, if you compile this (without the /debug+ switch) and you'll see that the TimerCallback method is called multiple times, and the program is fixed. What's happening here is that the object t is required to stay alive so the Dispose instance method can be called on it (The value in t needs to be passed as this argument to Dispose.)
