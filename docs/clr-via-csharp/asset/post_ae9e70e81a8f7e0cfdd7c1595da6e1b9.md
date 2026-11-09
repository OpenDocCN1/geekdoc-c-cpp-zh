
+   - **MonitoringTotalProcessorTime** This instance `TimeSpan` property returns the amount of CPU usage incurred by a specific AppDomain.

The following class shows how to use three of these properties to see what has changed within an AppDomain between two points in time:

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

The following code shows how to use the AppDomainMonitorDelta class:

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

When I execute this code, I get the following output:

```text
FriendlyName=03-Ch22-1-AppDomains.exe, CPU=5031.25ms
   Allocated 30,159,496 bytes of which 10,085,080 survived GCs
```

## AppDomain First-Chance Exception Notifications

Each AppDomain can have associated with it a series of callback methods that get invoked when the CLR begins looking for **catch** blocks within an AppDomain. These methods can perform logging, or a host can use this mechanism to monitor exceptions being thrown within an AppDomain. The callbacks cannot handle the exception or swallow it in any way; they are just receiving a notification that the exception has occurred. To register a callback method, just add a delegate to AppDomain's instance **FirstChanceException** event.

Here is how the CLR processes an exception: When the exception is first thrown, the CLR invokes any **FirstChanceException** callback methods registered with the AppDomain that is throwing the exception. Then, the CLR looks for any **catch** blocks on the stack that are within the same AppDomain. If a **catch** block handles the exception, then processing of the exception is complete and execution continues as normal. If the AppDomain has no **catch** block to handle the exception, then the CLR walks up the stack to the calling AppDomain and throws the same exception object again (after serializing and deserializing it). At this point, it is as if a brand new exception is being thrown, and the CLR invokes any **FirstChanceException** callback methods registered with the now current AppDomain. This continues until the top of the thread's stack is reached. At that point, if the exception is not handled by any code, the CLR terminates the whole process.

## How Hosts Use AppDomains

So far, I've talked about hosts and how they load the CLR. I've also talked about how the hosts tell the CLR to create and unload AppDomains. To make the discussion more concrete, I'll describe some common hosting and AppDomain scenarios. In particular, I'll explain how different application types host the CLR and how they manage AppDomains.

### Executable Applications

Console UI applications, NT Service applications, Windows Forms applications, and Windows Presentation Foundation (WPF) applications are all examples of self-hosted applications that have managed EXE files. When Windows initializes a process using a managed EXE file, Windows loads the shim and the shim examines the CLR header information contained in the application's assembly (the EXE file). The header information indicates the version of the CLR that was used to build and test the application. The shim uses this information to determine which version of the CLR to load into the process. After the CLR loads and initializes, it again examines the assembly's CLR header to determine which method is the application's entry point (**Main**). The CLR invokes this method, and the application is now up and running.

As the code runs, it accesses other types. When referencing a type contained in another assembly, the CLR locates the necessary assembly and loads it into the same AppDomain. Any additionally referenced assemblies also load into the same AppDomain. When the application's `Main` method returns, the Windows process terminates (destroying the default AppDomain and all other AppDomains).

> **Note** By the way, you can call `System.Environment`'s static `Exit` method if you want to shut down the Windows process including all of its AppDomains. `Exit` is the most graceful way of terminating a process because it first calls the `Finalize` methods of all of the objects on the managed heap and then releases all of the unmanaged COM objects held by the CLR. Finally, `Exit` calls the `Win32 ExitProcess` function.

It's possible for the application to tell the CLR to create additional AppDomains in the process's address space. In fact, this is what my Ch22-1-AppDomains application did.

## Microsoft Silverlight Rich Internet Applications

Microsoft's Silverlight runtime technology uses a special CLR that is different from the normal desktop version of the .NET Framework. Once the Silverlight runtime is installed, navigating to a Web site that uses Silverlight causes the Silverlight CLR (`CoreClr.dll`) to load in your browser (which may or may not be Windows Internet Explorer—you may not even be using a Windows machine). Each Silverlight control on the page runs in its own AppDomain. When the user closes a tab or navigates to another Web site, any Silverlight controls no longer in use have their AppDomains unloaded. The Silverlight code running in the AppDomain runs in a limited-security sandbox so that it cannot harm the user or the machine in any way.

## Microsoft ASP.NET Web Forms and XML Web Services Applications

ASP.NET is implemented as an ISAPI DLL (implemented in `ASPNET_ISAPI.dll`). The first time a client requests a URL handled by the ASP.NET ISAPI DLL, ASP.NET loads the CLR. When a client makes a request of a Web application, ASP.NET determines if this is the first time a request has been made. If it is, ASP.NET tells the CLR to create a new AppDomain for this Web application; each Web application is identified by its virtual root directory. ASP.NET then tells the CLR to load the assembly that contains the type exposed by the Web application into this new AppDomain, creates an instance of this type, and starts calling methods in it to satisfy the client's Web request. If the code references more types, the CLR will load the required assemblies into the Web application's AppDomain.

When future clients make requests of an already running Web application, ASP.NET doesn’t create a new AppDomain; instead, it uses the existing AppDomain, creates a new instance of the Web application’s type, and starts calling methods. The methods will already be JIT-compiled into native code, so the performance of processing all subsequent client requests is excellent.

If a client makes a request of a different Web application, ASP.NET tells the CLR to create a new AppDomain. This new AppDomain is typically created inside the same worker process as the other AppDomains. This means that many Web applications run in a single Windows process, which improves the efficiency of the system overall. Again, the assemblies required by each Web application are loaded into an AppDomain created for the sole purpose of isolating that Web application’s code and objects from other Web applications.

A fantastic feature of ASP.NET is that the code for a Web site can be changed on the fly without shutting down the Web server. When a Web site’s file is changed on the hard disk, ASP.NET detects this, unloads the AppDomain that contains the old version of the files (when the last currently running request finishes), and then creates a new AppDomain, loading into it the new versions of the files. To make this happen, ASP.NET uses an AppDomain feature called *shadow copying*.

## Microsoft SQL Server

Microsoft SQL Server is an unmanaged application because most of its code is still written in unmanaged C++. SQL Server allows developers to create stored procedures by using managed code. The first time a request comes in to the database to run a stored procedure written in managed code, SQL Server loads the CLR. Stored procedures run in their own secured AppDomain, prohibiting the stored procedures from adversely affecting the database server.

This functionality is absolutely incredible! It means that developers will be able to write stored procedures in the programming language of their choice. The stored procedure can use strongly typed data objects in its code. The code will also be JIT-compiled into native code when executed instead of being interpreted. And developers can take advantage of any types defined in the Framework Class Library (FCL) or in any other assembly. The result is that our job becomes much easier and our applications perform much better. What more could a developer ask for?!

## Your Own Imagination

Productivity applications such as word processors and spreadsheets also allow users to write macros in any programming language they choose. These macros will have access to all of the assemblies and types that work with the CLR. They will be compiled, so they will execute fast, and, most important, these macros will run in a secure AppDomain so that users don’t get hit with any unwanted surprises. Your own applications can use this ability, too, in any way you want.
