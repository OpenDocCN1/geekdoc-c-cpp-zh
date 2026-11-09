
JIT compiler–produced tables require a lot of memory and increase the working set, which in turn hurts performance significantly. So, the JIT compiler–produced tables contain information for sections of code having loops that do not call other methods. If the method has a loop that calls other methods or if there are no loops, the JIT compiler–produced tables do not have much information in them, and hijacking is used to suspend the threads.

## Garbage Collection Modes

When the CLR starts, it selects a GC mode, and this mode cannot change during the lifetime of the process. There are two basic GC modes:

- **Workstation** This mode fine-tunes the garbage collector for client-side applications. The garbage collector assumes that other applications are running on the machine and does not hog CPU resources. The Workstation mode can have two submodes: Workstation with the concurrent collector and Workstation without the concurrent collector. I’ll describe the concurrent collector feature shortly.
- **Server** This mode fine-tunes the garbage collector for server-side applications. The garbage collector assumes that no other applications (client or server) are running on the machine and it assumes that all the CPUs on the machine are available to do a garbage collection. This GC mode causes the managed heap to be split into several sections, one per CPU. When a garbage collection is initiated, the garbage collector has one thread per CPU; each thread collects its own section in parallel with the other threads. Parallel collections work well for server applications in which the worker threads tend to exhibit uniform behavior. This feature requires the application to be running on a computer with multiple CPUs so that the threads can truly be working simultaneously to attain a performance improvement.

By default, applications run with the Workstation GC mode, and the concurrent collector is turned on. However, a server application (such as ASP.NET or SQL Server) that hosts the CLR can request the CLR to load the Server GC. However, if the server application is running on a uniprocessor machine, then the CLR will load the Workstation GC mode with the concurrent collector.

An application that self-hosts the CLR can tell the CLR to use the server collector by creating a configuration file (as discussed in Chapter 2, “Building, Packaging, Deploying, and Administering Applications and Types,” and Chapter 3, “Shared Assemblies and Strongly Named Assemblies”) that contains a **gcServer** element for the application. Here’s an example of a configuration file:

```xml
<configuration>
    <runtime>
        <gcServer enabled="true"/>
    </runtime>
</configuration>
```

When an application is running, it can ask the CLR if it is running in the Server GC mode by querying the GCSettings class's IsServerGC read-only Boolean property:

```csharp
using System;
using System.Runtime; // GCSettings is in this namespace

public static class Program {
    public static void Main() {
        Console.WriteLine("Application is running with server GC=" + GCSettings.IsServerGC);
    }
}
```

The Workstation GC mode can run in concurrent or non-concurrent mode. In concurrent mode, the garbage collector has an additional background thread that collects objects concurrently while the application runs. When a thread allocates an object that pushes generation 0 over its budget, the garbage collector first suspends all threads and then determines which generations to collect. If the garbage collector needs to collect generation 0 or 1, it proceeds as normal. However, if generation 2 needs collecting, the size of generation 0 will be increased beyond its budget to allocate the new object, and then the application's threads are resumed.

While the application's threads are running, the garbage collector has a normal priority background thread that marks unreachable objects. This thread competes for CPU time with the application's threads, causing the application's tasks to execute more slowly. Once the objects are marked, the garbage collector suspends all threads again and decides whether to compact memory. If the garbage collector decides to compact memory, memory is compacted, root references are fixed up, and the application's threads are resumed. This garbage collection takes less time than usual because the set of unreachable objects has already been built. However, the garbage collector might decide not to compact memory; in fact, the garbage collector favors this approach. If you have a lot of free memory, the garbage collector won't compact the heap; this improves performance but grows your application's working set. When using the concurrent garbage collector, you'll typically find that your application is consuming more memory than it would with the non-concurrent garbage collector.

To summarize: Concurrent collection creates a better interactive experience for users and is therefore best for interactive CUI or GUI applications. For some applications, however, concurrent collection will actually hurt performance and will cause more memory to be used. When testing your application, you should experiment with and without concurrent collection and see which approach gives the best performance and memory usage for your application.

You can tell the CLR not to use the concurrent collector by creating a configuration file for the application (as discussed in Chapters 2 and 3) that contains a gcConcurrent element. Here's an example of a configuration file:

manipulating this setting. Here is some code showing how to properly use the **LowLatency** mode:

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

## Large Objects

There is one more performance improvement you might want to be aware of. Any objects that are 85,000 bytes or more in size are considered to be *large objects*. Large objects are allocated from a special large object heap. Objects in this heap are finalized and freed just as the small objects I've been talking about. However, large objects are never compacted because it would waste too much CPU time to shift 85,000-byte blocks of memory down in the heap. However, you should never write code that assumes that large objects do not move in memory because the size of large objects could change from 85,000 bytes to something else in the future. To guarantee that an object doesn't move in memory, pin it as discussed in the "Monitoring and Controlling the Lifetime of Objects Manually" section earlier in this chapter.

Large objects are always considered part of generation 2, so you should create large objects only for resources that you need to keep alive for a long time. Allocating short-lived large objects will cause generation 2 to be collected more frequently, which will hurt performance. The following program proves that large objects are always allocated in generation 2:

```csharp
using System;

public static class Program {
    public static void Main() {
        Object o = new Byte[85000];
        Console.WriteLine(GC.GetGeneration(o));   // Displays 2; not 0
    }
}
```

All of these mechanisms are transparent to your application code. To you, the developer, it appears as if there is just one managed heap; these mechanisms exist simply to improve application performance.

## Monitoring Garbage Collections

Within a process, there are a few methods that you can call to monitor the garbage collector. Specifically, the GC class offers the following static methods, which you can call to see how many collections have occurred of a specific generation or how much memory is currently being used by objects in the managed heap.

```
Int64 GetTotalMemory(Boolean forceFullCollection);
Int32 CollectionCount(Int32 generation);
```

To profile a particular code block, I have frequently written code to call these methods before and after the code block and then calculate the difference. This gives me a very good indication of how my code block has affected my process's working set and indicates how many garbage collections occurred while executing the code block. If the numbers are high, I know to spend more time tuning the algorithms in my code block.

You can also see how much memory is being used by individual AppDomains as opposed to the whole process. For more information about this, see the "AppDomain Monitoring" section in Chapter 22.

When you install the .NET Framework, it installs a set of performance counters that offer a lot of real-time statistics about the CLR's operations. These statistics are visible via the PerfMon.exe tool or the System Monitor ActiveX control that ships with Windows. The easiest way to access the System Monitor control is to run PerfMon.exe and click the + toolbar button, which causes the Add Counters dialog box shown in Figure 21-16 to appear.

![](img/3c46ff5b170881db4209d365b1f7a808_606_0.png)

**FIGURE 21-16** PerfMon.exe showing the .NET CLR Memory counters
