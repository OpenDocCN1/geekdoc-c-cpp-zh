
Your code might try to catch it and recover from it, but you didn’t even know you were invoking the type constructor. So the CLR converts the DivideByZeroException into a TypeInitializationException so that you know clearly that the exception occurred due to a type constructor failing; the problem wasn’t with your code.

On the other hand, here is a bad use of this technique: when you invoke a method via reflection, the CLR then wraps each exception thrown by the method and converts it to a TargetInvocationException. This is incredibly annoying because you must now catch the TargetInvocationException object and look at its InnerException property to discern the real reason for the failure. In fact, when using reflection, it is common to see code that looks like this.

```csharp
private static void Reflection(Object o) {
    try {
        // Invoke a DoSomething method on this object
        var mi = o.GetType().GetMethod("DoSomething");
        mi.Invoke(o, null); // The DoSomething method might throw an exception
    }
    catch (System.Reflection.TargetInvocationException e) {
        // The CLR converts reflection-produced exceptions to TargetInvocationException
        throw e.InnerException; // Re-throw what was originally thrown
    }
}
```

I have good news though: if you use C#’s dynamic primitive type (discussed in Chapter 5, “Primitive, Reference, and Value Types”) to invoke a member, the compiler-generated code does not catch any and all exceptions and throw a TargetInvocationException object; the original thrown exception object simply walks up the stack. For many developers, this is a good reason to prefer using C#’s dynamic primitive type rather than reflection.

## Unhandled Exceptions

When an exception is thrown, the CLR climbs up the call stack looking for catch blocks that match the type of the exception object being thrown. If no catch block matches the thrown exception type, an unhandled exception occurs. When the CLR detects that any thread in the process has had an unhandled exception, the CLR terminates the process. An unhandled exception identifies a situation that the application didn’t anticipate and is considered to be a true bug in the application. At this point, the bug should be reported back to the company that publishes the application. Hopefully, the publisher will fix the bug and distribute a new version of the application.

Class library developers should not even think about unhandled exceptions. Only application developers need to concern themselves with unhandled exceptions, and the application should have a policy in place for dealing with unhandled exceptions. Microsoft actually recommends that application developers just accept the CLR’s default policy. That is, when an application gets an unhandled exception, Windows writes an entry to the system’s event log. You can see this entry by opening the Event Viewer application and then looking under the Windows Logs ➞ Application node in the tree, as shown in Figure 20-1.

![](img/857bdf6cef9e242b53a37f88df9a1287_511_0.png)

**FIGURE 20-1** Windows Event log showing an application that terminated due to an unhandled exception.

However, you can get more interesting details about the problem by using the Windows Reliability Monitor applet. To start Reliability Monitor, open the Windows Control Panel and search for "reliability history." From here, you can see the applications that have terminated due to an unhandled exception in the bottom pane, as shown in Figure 20-2.

![](img/857bdf6cef9e242b53a37f88df9a1287_511_1.png)

**FIGURE 20-2** Reliability Monitor showing an application that terminated due to an unhandled exception.

To see more details about the terminated application, double-click a terminated application in Reliability Monitor. The details will look something like Figure 20-3 and the meaning of the problem signatures are described in Table 20-2. All unhandled exceptions produced by managed applications are placed in the CLR20r3 bucket.

![](img/857bdf6cef9e242b53a37f88df9a1287_512_0.png)

**FIGURE 20-3** Reliability Monitor showing more details about the failed application.

### TABLE 20-2 Problem Signatures

| Problem Signature | Description* |
|---|---|
| 01 | EXE file's name (32-character limit) |
| 02 | EXE file's assembly version number |
| 03 | EXE file's timestamp |
| 04 | EXE file's full assembly name (64-character limit) |
| 05 | Faulting assembly's version |
| 06 | Faulting assembly's timestamp |
| 07 | Faulting assembly's type and method. This value is a MethodDef metadata token (after stripping off the 0x06 high byte) identifying the method that threw the exception. From this value, you can use ILDasm.exe to determine the offending type and method. |
| 08 | Faulting method's IL instruction. This value is an offset within the faulting method of the IL instruction that threw the exception. From this value, you can use ILDasm.exe to determine the offending instruction. |
| 09 | Exception type thrown (32-character limit) |

* If a string is beyond the allowed limit, then some intelligent truncations are performed, like removing “Exception” from the exception type or “.dll” from a file name. If the resulting string is still too long, then the CLR will create a value by hashing or base-64-encoding the string.

After recording information about the failing application, Windows displays the message box allowing the end user to send information about the failing application to Microsoft servers.⁷ This is called *Windows Error Reporting*, and more information about it can be found at the Windows Quality website (http://WinQual.Microsoft.com).

Companies can optionally sign up with Microsoft to view this information about their own applications and components. Signing up is free, but it does require that your assemblies be signed with a VeriSign ID (also called a Software Publisher’s Digital ID for Authenticode).

Naturally, you could also develop your own system for getting unhandled exception information back to you so that you can fix bugs in your code. When your application initializes, you can inform the CLR that you have a method that you want to be called whenever any thread in your application experiences an unhandled exception.

Unfortunately, every application model Microsoft produces has its own way of tapping into unhandled exceptions. The members that you want to look up in the FCL documentation are:

- For many applications, look at `System.AppDomain`’s `UnhandledException` event. Windows Store applications and Microsoft Silverlight applications cannot access this event.
- For a Windows Store App, look at `Windows.UI.Xaml.Application`’s `UnhandledException` event.
- For a Windows Forms application, look at `System.Windows.Forms.NativeWindow`’s `OnThreadException` virtual method, `System.Windows.Forms.Application`’s `OnThreadException` virtual method, and `System.Windows.Forms.Application`’s `ThreadException` event.
- For a Windows Presentation Foundation (WPF) application, look at `System.Windows.Application`’s `DispatcherUnhandledException` event and `System.Windows.Threading.Dispatcher`’s `UnhandledException` and `UnhandledExceptionFilter` events.
- For Silverlight, look at `System.Windows.Application`’s `UnhandledException` event.
- For an ASP.NET Web Form application, look at `System.Web.UI.TemplateControl`’s `Error` event. `TemplateControl` is the base class of the `System.Web.UI.Page` and `System.Web.UI.UserControl` classes. Furthermore, you should also look at `System.Web.HttpApplication`’s `Error` event.
- For a Windows Communication Foundation application, look at `System.ServiceModel.Dispatcher.ChannelDispatcher`’s `ErrorHandlers` property.

Before I leave this section, I’d like to say a few words about unhandled exceptions that could occur in a distributed application such as a website or web service. In an ideal world, a server application that experiences an unhandled exception should log it, send some kind of notification back to the

⁷ You can actually disable this message box by using P/Invoke to call Win32’s `SetErrorMode` function, passing in `SEM_NOGPFAULTERRORBOX`.
