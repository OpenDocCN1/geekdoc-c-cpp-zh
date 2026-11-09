manipulating this setting. Here is some code showing how to properly use the **LowLatency** mode:

```
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
```

# ## Large Objects

There is one more performance improvement you might want to be aware of. Any objects that are 85,000 bytes or more in size are considered to be *large objects*. Large objects are allocated from a special large object heap. Objects in this heap are finalized and freed just as the small objects I've been talking about. However, large objects are never compacted because it would waste too much CPU time to shift 85,000-byte blocks of memory down in the heap. However, you should never write code that assumes that large objects do not move in memory because the size of large objects could change from 85,000 bytes to something else in the future. To guarantee that an object doesn't move in memory, pin it as discussed in the "Monitoring and Controlling the Lifetime of Objects Manually" section earlier in this chapter.

Large objects are always considered part of generation 2, so you should create large objects only for resources that you need to keep alive for a long time. Allocating short-lived large objects will cause generation 2 to be collected more frequently, which will hurt performance. The following program proves that large objects are always allocated in generation 2:

```
```csharp
using System;

public static class Program {
    public static void Main() {
        Object o = new Byte[85000];
        Console.WriteLine(GC.GetGeneration(o));   // Displays 2; not 0
    }
}
```
```

All of these mechanisms are transparent to your application code. To you, the developer, it appears as if there is just one managed heap; these mechanisms exist simply to improve application performance.