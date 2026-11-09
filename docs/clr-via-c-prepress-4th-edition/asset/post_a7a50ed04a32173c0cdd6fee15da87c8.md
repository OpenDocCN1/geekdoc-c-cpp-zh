
generations as well to improve the overall performance of the application. The end result is that the garbage collector fine-tunes itself automatically based on the memory load required by your application—this is very cool!

The GCNotification class shown below raises an event whenever a generation 0 or generation 2 collection occurs. With these events, you could have the computer beep whenever a collection occurs or you calculate how much time passes between collections, how much memory is allocated between collections, and more. With this class, you could easily instrument your application to get a better understanding of how your application uses memory.

```csharp
public static class GCNotification {
    private static Action<Int32> s_gcDone = null;   // The event's field

    public static event Action<Int32> GCDone {
        add {
            // If there were no registered delegates before, start reporting notifications now
            if (s_gcDone == null) { new GenObject(0); new GenObject(2); }
            s_gcDone += value;
        }
        remove { s_gcDone -= value; }
    }

    private sealed class GenObject {
        private Int32 m_generation;
        public GenObject(Int32 generation) { m_generation = generation; }
        ~GenObject() { // This is the Finalize method
            // If this object is in the generation we want (or higher),
            // notify the delegates that a GC just completed
            if (GC.GetGeneration(this) >= m_generation) {
                Action<Int32> temp = Volatile.Read(ref s_gcDone);
                if (temp != null) temp(m_generation);
            }

            // Keep reporting notifications if there is at least one delegate registered,
            // the AppDomain isn't unloading, and the process isn't shutting down
            if ((s_gcDone != null)
                && !AppDomain.CurrentDomain.IsFinalizingForUnload()
                && !Environment.HasShutdownStarted) {
                // For Gen 0, create a new object; for Gen 2, resurrect the object
                // & let the GC call Finalize again the next time Gen 2 is GC'd
                if (m_generation == 0) new GenObject(0);
                else GC.ReRegisterForFinalize(this);
            } else { /* Let the objects go away */ }
        }
    }
}
```

## GC Triggers

As you know, the CLR triggers a GC when it detects that generation 0 has filled its budget. This is the most common trigger of a GC; however, there are additional GC triggers as listed below:

```csharp
public static class Program {
    public static void Main() {
        Console.WriteLine("Application is running with server GC=" + GCSettings.IsServerGC);
    }
}
```

In addition to the two modes, the GC can run in two sub-modes: concurrent (the default) or non-concurrent. In concurrent mode, the GC has an additional background thread that marks objects concurrently while the application runs. When a thread allocates an object that pushes generation 0 over its budget, the GC first suspends all threads and then determines which generations to collect. If the garbage collector needs to collect generation 0 or 1, it proceeds as normal. However, if generation 2 needs collecting, the size of generation 0 will be increased beyond its budget to allocate the new object, and then the application’s threads are resumed.

While the application’s threads are running, the garbage collector has a normal priority background thread that finds unreachable objects. Once found, the garbage collector suspends all threads again and decides whether to compact memory. If the garbage collector decides to compact memory, memory is compacted, root references are fixed up, and the application’s threads are resumed. This garbage collection takes less time than usual because the set of unreachable objects has already been built. However, the garbage collector might decide not to compact memory; in fact, the garbage collector favors this approach. If you have a lot of free memory, the garbage collector won’t compact the heap; this improves performance but grows your application’s working set. When using the concurrent garbage collector, you’ll typically find that your application is consuming more memory than it would with the non-concurrent garbage collector.

You can tell the CLR not to use the concurrent collector by creating a configuration file for the application that contains a gcConcurrent element. Here’s an example of a configuration file:

```xml
<configuration>
    <runtime>
        <gcConcurrent enabled="false"/>
    </runtime>
</configuration>
```

The GC mode is configured for a process and it cannot change while the process runs. However, your application can have some control over the garbage collection by using the GCSettings class’s GCLatencyMode property. This read/write property can be set to any of the values in the GCLatencyMode enumerated type, as shown in Table 21-1.

TABLE 21-1 Symbols Defined by the GCLatencyMode Enumerated Type

| Symbol Name | Description |
|---|---|
| Batch (default for the Server GC mode) | Turns off the concurrent GC. |
| Interactive (default for the Workstation GC mode) | Turns on the concurrent GC. |
| LowLatency | Use this latency mode during short-term, time-sensitive operations (like drawing animations) where a generation 2 collection might be disruptive. |
| SustainedLowLatency | Use this latency mode to avoid long GC pauses for the bulk of your application’s execution. This setting prevents all blocking generation 2 collections from occurring as long as memory is available. In fact, users of these applications would prefer to install more RAM in the machine in order to avoid GC pauses. A stock market application that must respond immediately to price changes is an example of this kind of application. |

The LowLatency mode requires some additional explanation. Typically, you would set this mode, perform a short-term, time-sensitive operation, and then set the mode back to either Batch or Interactive. While the mode is set to LowLatency, the GC will really avoid doing any generation 2 collections because these could take a long time. Of course, if you call GC.Collect(), then generation 2 still gets collected. Also, the GC will perform a generation 2 collection if Windows tells the CLR that system memory is low (see the “GC Triggers” section earlier in this chapter).

Under LowLatency mode, it is more likely that your application could get an OutOfMemoryException thrown. Therefore, stay in this mode for as short a time as possible, avoid allocating many objects, avoid allocating large objects, and set the mode back to Batch or Interactive using a constrained execution region (CER), as discussed in Chapter 20, “Exceptions and State Management.” Also, remember that the latency mode is a process-wide setting and threads may be running concurrently. These other threads could even change this setting while another thread is using it and so you may want to update some kind of counter (manipulated via Interlocked methods) when you have multiple threads manipulating this setting. Here is some code showing how to use the LowLatency mode:

```csharp
    private static void LowLatencyDemo() {
        GCLatencyMode oldMode = GCSettings.LatencyMode;
        System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions();
        try {
            GCSettings.LatencyMode = GCLatencyMode.LowLatency;
            // Run your code here...
        }
        finally {
            GCSettings.LatencyMode = oldMode;
        }
    }
```

## Forcing Garbage Collections

The System.GC type allows your application some direct control over the garbage collector. For starters, you can query the maximum generation supported by the managed heap by reading the GC.MaxGeneration property; this property always returns 2.

You can also force the garbage collector to perform a collection by calling GC class’s Collect method optionally passing in a generation to collect up to, a GCCollectionMode, and a Boolean indicating if you want to perform a blocking (non-current) or background (concurrent) collection. Here is the signature of the most complex overload of the Collect method:

```csharp
void Collect(Int32 generation, GCCollectionMode mode, Boolean blocking);
```

The GCCollectionMode type is an enum whose values are described in Table 21-2.

TABLE 21-2 Symbols Defined by the GCCollectionMode Enumerated Type

| Symbol Name | Description |
|---|---|
| Default | The same as calling `GC.Collect` with no flag. Today, this is the same as passing Forced, but this may change in a future version of the CLR. |
| Forced | Forces a collection to occur immediately for all generations up to and including the specified generation. |
| Optimized | The garbage collector will only perform a collection if the collection would be productive either by freeing a lot of memory or by reducing fragmentation. If the garbage collection would not be productive, then the call has no effect. |

**Under most circumstances, you should avoid calling any of the Collect methods;** it’s best just to let the garbage collector run on its own accord and fine-tune its generation budgets based on actual application behavior. However, if you’re writing a console user interface (CUI) or graphical user interface (GUI) application, your application code owns the process and the CLR in that process. For these application types, you *might* want to suggest a garbage collection to occur at certain times using a GCCollectionMode of Optimized. Normally, modes of Default and Forced are used for debugging, testing, and looking for memory leaks.

For example, you might consider calling the Collect method if some non-recurring event has just occurred that has likely caused a lot of old objects to die. The reason that calling Collect in such a circumstance may not be so bad is that the GC’s predictions of the future based on the past are not likely to be accurate for non-recurring events. For example, it might make sense for your application to force a full GC of all generations after your application initializes or after the user saves a data file. Since calling Collect causes the generation budgets to adjust, do not call Collect to try to improve your application’s response time; call it to reduce your process’s working set.

For some applications (especially server applications that tend to keep a lot of objects in memory), the time required for the GC to do a full collection that includes generation 2 can be excessive. In fact, if the collection takes a very long time to complete, then client requests might time out. To help these kinds of applications, the GC class offers a RegisterForFullGCNotification method. Using this method and some additional helper methods (WaitForFullGCApproach, WaitForFullGCComplete,
