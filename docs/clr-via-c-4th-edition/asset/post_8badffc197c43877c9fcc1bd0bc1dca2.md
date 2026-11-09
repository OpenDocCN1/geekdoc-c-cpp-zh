
- 3. After all threads discovered in step 2 have left the AppDomain, the CLR then walks the heap and sets a flag in each proxy object that referred to an object created by the unloaded AppDomain. These proxy objects now know that the real object they referred to is gone. If any code now calls a method on an invalid proxy object, the method will throw an `AppDomainUnloadedException`.
- 4. The CLR forces a garbage collection to occur, reclaiming the memory used by any objects that were created by the now unloaded AppDomain. The `Finalize` methods for these objects are called, giving the objects a chance to clean themselves up properly.
- 5. The CLR resumes all of the remaining threads. The thread that called `AppDomain.Unload` will now continue running; calls to `AppDomain.Unload` occur synchronously.

My Ch22-1-AppDomains application uses just one thread to do all of the work. Whenever my code calls `AppDomain.Unload`, there are no threads in the unloading AppDomain, and therefore, the CLR doesn't have to throw any `ThreadAbortException` exceptions. I'll talk more about `ThreadAbortException` later in this chapter.

By the way, when a thread calls `AppDomain.Unload`, the CLR waits 10 seconds for the threads in the unloading AppDomain to leave it. If after 10 seconds, the thread that called `AppDomain.Unload` doesn't return, it will throw a `CannotUnloadAppDomainException`, and the AppDomain may or may not be unloaded in the future.

> **Note** If a thread calling `AppDomain.Unload` is in the AppDomain being unloaded, the CLR creates another thread that attempts to unload the AppDomain. The first thread will forcibly throw the `ThreadAbortException` and unwind. The new thread will wait for the AppDomain to unload, and then the new thread terminates. If the AppDomain fails to unload, the new thread will process a `CannotUnloadAppDomainException`, but because you did not write the code that this new thread executes, you can't catch this exception.

## AppDomain Monitoring

A host application can monitor the resources that an AppDomain consumes. Some hosts will use this information to decide when to forcibly unload an AppDomain should its memory or CPU consumption rise above what the host considers reasonable. Monitoring can also be used to compare the resource consumption of different algorithms to determine which uses fewer resources. Because AppDomain monitoring incurs additional overhead, hosts must explicitly turn the monitoring on by setting `AppDomain`'s static `MonitoringIsEnabled` property to `true`. This turns on monitoring for all AppDomains. After monitoring is turned on, it cannot be turned off; attempting to set the `MonitoringIsEnabled` property to `false` causes an `ArgumentException` to be thrown.

After monitoring is turned on, your code can query the following four read-only properties offered by the AppDomain class:

- **MonitoringSurvivedProcessMemorySize** This static Int64 property returns the number of bytes that are currently in use by all AppDomains controlled by the current CLR instance. The number is accurate as of the last garbage collection.
- **MonitoringTotalAllocatedMemorySize** This instance Int64 property returns the number of bytes that have been allocated by a specific AppDomain. The number is accurate as of the last garbage collection.
- **MonitoringSurvivedMemorySize** This instance Int64 property returns the number of bytes that are currently in use by a specific AppDomain. The number is accurate as of the last garbage collection.
- **MonitoringTotalProcessorTime** This instance TimeSpan property returns the amount of CPU usage incurred by a specific AppDomain.

The following class shows how to use three of these properties to see what has changed within an AppDomain between two points in time.

```csharp
private sealed class AppDomainMonitorDelta : IDisposable {
    private AppDomain m_appDomain;
    private TimeSpan m_thisADCpu;
    private Int64 m_thisADMemoryInUse;
    private Int64 m_thisADMemoryAllocated;

    static AppDomainMonitorDelta() {
        // Make sure that AppDomain monitoring is turned on
        AppDomain.MonitoringIsEnabled = true;
    }

    public AppDomainMonitorDelta(AppDomain ad) {
        m_appDomain = ad ?? AppDomain.CurrentDomain;
        m_thisADCpu = m_appDomain.MonitoringTotalProcessorTime;
        m_thisADMemoryInUse = m_appDomain.MonitoringSurvivedMemorySize;
        m_thisADMemoryAllocated = m_appDomain.MonitoringTotalAllocatedMemorySize;
    }

    public void Dispose() {
        GC.Collect();
        Console.WriteLine("FriendlyName={0}, CPU={1}ms", m_appDomain.FriendlyName,
            (m_appDomain.MonitoringTotalProcessorTime - m_thisADCpu).TotalMilliseconds);
        Console.WriteLine("   Allocated {0:N0} bytes of which {1:N0} survived GCs",
            m_appDomain.MonitoringTotalAllocatedMemorySize - m_thisADMemoryAllocated,
            m_appDomain.MonitoringSurvivedMemorySize - m_thisADMemoryInUse);
    }
}
```

The following code shows how to use the AppDomainMonitorDelta class.

```csharp
private static void AppDomainResourceMonitoring() {
   using (new AppDomainMonitorDelta(null)) {
      // Allocate about 10 million bytes that will survive collections
      var list = new List<Object>();
      for (Int32 x = 0; x < 1000; x++) list.Add(new Byte[10000]);

      // Allocate about 20 million bytes that will NOT survive collections
      for (Int32 x = 0; x < 2000; x++) new Byte[10000].GetType();

      // Spin the CPU for about 5 seconds
      Int64 stop = Environment.TickCount + 5000;
      while (Environment.TickCount < stop) ;
   }
}
```

When I execute this code, I get the following output.

```
FriendlyName=03-Ch22-1-AppDomains.exe, CPU=5031.25ms
   Allocated 30,159,496 bytes of which 10,085,080 survived GCs
```

## AppDomain First-Chance Exception Notifications

Each AppDomain can have associated with it a series of callback methods that get invoked when the CLR begins looking for catch blocks within an AppDomain. These methods can perform logging, or a host can use this mechanism to monitor exceptions being thrown within an AppDomain. The callbacks cannot handle the exception or swallow it in any way; they are just receiving a notification that the exception has occurred. To register a callback method, just add a delegate to AppDomain's instance FirstChanceException event.

Here is how the CLR processes an exception: when the exception is first thrown, the CLR invokes any FirstChanceException callback methods registered with the AppDomain that are throwing the exception. Then, the CLR looks for any catch blocks on the stack that are within the same AppDomain. If a catch block handles the exception, then processing of the exception is complete and execution continues as normal. If the AppDomain has no catch block to handle the exception, then the CLR walks up the stack to the calling AppDomain and throws the same exception object again (after serializing and deserializing it). At this point, it is as if a brand new exception is being thrown, and the CLR invokes any FirstChanceException callback methods registered with the new current AppDomain. This continues until the top of the thread's stack is reached. At that point, if the exception is not handled by any code, the CLR terminates the whole process.

## Microsoft ASP.NET and XML Web Services Applications

ASP.NET is implemented as an ISAPI DLL (implemented in ASPNET_ISAPI.dll). The first time a client requests a URL handled by the ASP.NET ISAPI DLL, ASP.NET loads the CLR. When a client makes a request of a web application, ASP.NET determines if this is the first time a request has been made. If it is, ASP.NET tells the CLR to create a new AppDomain for this web application; each web application is identified by its virtual root directory. ASP.NET then tells the CLR to load the assembly that contains the type exposed by the web application into this new AppDomain, creates an instance of this type, and starts calling methods in it to satisfy the client's web request. If the code references more types, the CLR will load the required assemblies into the web application's AppDomain.

When future clients make requests of an already running web application, ASP.NET doesn't create a new AppDomain; instead, it uses the existing AppDomain, creates a new instance of the web application's type, and starts calling methods. The methods will already be JIT-compiled into native code, so the performance of processing all subsequent client requests is excellent.

If a client makes a request of a different web application, ASP.NET tells the CLR to create a new AppDomain. This new AppDomain is typically created inside the same worker process as the other AppDomains. This means that many web applications run in a single Windows process, which improves the efficiency of the system overall. Again, the assemblies required by each web application are loaded into an AppDomain created for the sole purpose of isolating that web application's code and objects from other web applications.

A fantastic feature of ASP.NET is that the code for a website can be changed on the fly without shutting down the web server. When a website's file is changed on the hard disk, ASP.NET detects this, unloads the AppDomain that contains the old version of the files (when the last currently running request finishes), and then creates a new AppDomain, loading into it the new versions of the files. To make this happen, ASP.NET uses an AppDomain feature called *shadow copying*.

### Microsoft SQL Server

Microsoft SQL Server is an unmanaged application because most of its code is still written in unmanaged C++. SQL Server allows developers to create stored procedures by using managed code. The first time a request comes in to the database to run a stored procedure written in managed code, SQL Server loads the CLR. Stored procedures run in their own secured AppDomain, prohibiting the stored procedures from adversely affecting the database server.

This functionality is absolutely incredible! It means that developers will be able to write stored procedures in the programming language of their choice. The stored procedure can use strongly typed data objects in its code. The code will also be JIT-compiled into native code when executed instead of being interpreted. And developers can take advantage of any types defined in the Framework Class Library (FCL) or in any other assembly. The result is that our job becomes much easier and our applications perform much better. What more could a developer ask for?!
