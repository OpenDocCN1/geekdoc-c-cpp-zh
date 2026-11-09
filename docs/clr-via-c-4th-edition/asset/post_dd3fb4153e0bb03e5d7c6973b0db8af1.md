
- 4. This trusted code then enters a `try` block, and from within the `try` block, calls across an `AppDomain` boundary (via a type derived from `MarshalByRefObject`). This `AppDomain` contains the untrusted code (perhaps a stored procedure) that was not built and tested by the company that produced the host application. At this point, the server has given control of its thread to some untrusted code; the server is feeling nervous right now.
- 5. When the host originally received the client's request, it recorded the time. If the untrusted code doesn't respond to the client in some administrator-set amount of time, the host calls `Thread`'s `Abort` method, asking the CLR to stop the thread pool thread, forcing it to throw a `ThreadAbortException`.
- 6. At this point, the thread pool thread starts unwinding, calling `finally` blocks so that cleanup code executes. Eventually, the thread pool thread crosses back over the `AppDomain` boundary. Because the host's stub code called the untrusted code from inside a `try` block, the host's stub code has a `catch` block that catches the `ThreadAbortException`.
- 7. In response to catching the `ThreadAbortException`, the host calls `Thread`'s `ResetAbort` method. I'll explain the purpose of this call shortly.
- 8. Now that the host's code has caught the `ThreadAbortException`, the host can return some sort of failure back to the client and allow the thread pool thread to return to the pool so that it can be used for a future client request.

![](img/857bdf6cef9e242b53a37f88df9a1287_604_0.png)

**FIGURE 22-3** How a host application gets its thread back.

It should be noted, though, that most untrusted code is not actually intended to be malicious; it is just written in such a way so as to be taking too long by the host's standards. Usually, `catch` and `finally` blocks contain very little code, and this code usually executes quickly without any infinite loops or long-running tasks. And so it is very unlikely that the escalation policy will have to go into effect for the host to regain control of its thread.

By the way, the `Thread` class actually offers two `Abort` methods: one takes no parameters, and the other takes an `Object` parameter allowing you to pass anything. When code catches the `ThreadAbortException`, it can query its read-only `ExceptionState` property. This property returns the object that was passed to `Abort`. This allows the thread calling `Abort` to specify some additional information that can be examined by code catching the `ThreadAbortException`. The host can use this to let its own handling code know why it is aborting threads.

## CHAPTER 23

### Assembly Loading and Reflection

In this chapter:

- Assembly Loading ........ 584
- Using Reflection to Build a Dynamically Extensible Application ........ 588
- Reflection Performance ........ 589
- Designing an Application That Supports Add-Ins ........ 596
- Using Reflection to Discover a Type's Members ........ 599

This chapter is all about discovering information about types, creating instances of them, and accessing their members when you didn’t know anything about them at compile time. The information in this chapter is typically used to create a dynamically extensible application. This is the kind of application for which one company builds a host application and other companies create add-ins to extend the host application. The host can’t be built or tested against the add-ins because the add-ins are created by different companies and are likely to be created after the host application has already shipped. This is why the host needs to discover the add-ins at run time.

A dynamically extensible application could take advantage of common language runtime (CLR) hosting and AppDomains as discussed in Chapter 22, “CLR Hosting and AppDomains.” The host could run the add-in code in an AppDomain with its own security and configuration settings. The host could also unload the add-in code by unloading the AppDomain. At the end of this chapter, I’ll talk a little about how to put all of this stuff together—CLR hosting, AppDomains, assembly loading, type discovery, type instance construction, and reflection—in order to build a robust, secure, and dynamically extensible application.

> **Important** For version 4.5 of the .NET Framework, Microsoft has introduced a new reflection API. The old API had many shortcomings. For example, it did not support LINQ well, it had policies embedded in it that were not correct for some languages, it would sometimes force the loading of assemblies unnecessarily, and it was an overly complex API that offered solutions for problems rarely encountered. The new API fixes all of these issues. However, as of .NET 4.5, the new reflection API is not as complete as the old API. With the new API and some extension methods (in the System.Reflection.RuntimeReflectionExtensions class), you can accomplish all you need. Expect additional methods to be added to the new API in future versions of the .NET Framework.

Of course, for desktop applications, the old API still exists so that it doesn't break existing code when re-compiling it. However, the new API is the recommended API going forward, and that is why I explain the new API exclusively in this chapter. For Windows Store Apps (where backward compatibility is not an issue), using the new API is mandatory.

### Assembly Loading

As you know, when the just-in-time (JIT) compiler compiles the Intermediate Language (IL) for a method, it sees what types are referenced in the IL code. Then at run time, the JIT compiler uses the assembly's TypeRef and AssemblyRef metadata tables to determine what assembly defines the type being referenced. The AssemblyRef metadata table entry contains all of the parts that make up the strong name of the assembly. The JIT compiler grabs all of these parts—name (without extension or path), version, culture, and public key token—concatenates them into a string, and then attempts to load an assembly matching this identity into the AppDomain (assuming that it's not already loaded). If the assembly being loaded is weakly named, the identity is just the name of the assembly (no version, culture, or public key token information).

Internally, the CLR attempts to load this assembly by using the System.Reflection.Assembly class's static Load method. This method is publicly documented, and you can call it to explicitly load an assembly into your AppDomain. This method is the CLR equivalent of Win32's LoadLibrary function. There are actually several overloaded versions of Assembly's Load method. Here are the prototypes of the more commonly used overloads.

```csharp
public class Assembly {
   public static Assembly Load(AssemblyName assemblyRef);
   public static Assembly Load(String assemblyString);
   // Less commonly used overloads of Load are not shown
}
```

Internally, Load causes the CLR to apply a version-binding redirection policy to the assembly and looks for the assembly in the global assembly cache (GAC), followed by the application's base directory, private path subdirectories, and codebase locations. If you call Load by passing a weakly named assembly, Load doesn't apply a version-binding redirection policy to the assembly, and the CLR won't look in the GAC for the assembly. If Load finds the specified assembly, it returns a reference to an Assembly object that represents the loaded assembly. If Load fails to find the specified assembly, it throws a System.IO.FileNotFoundException.

> **Note** In some extremely rare situations, you may want to load an assembly that was built for a specific CPU architecture. In this case, when specifying an assembly's identity, you can also include a process architecture part. For example, if my GAC happened to have an IL-neutral and an x86-specific version of an assembly, the CLR would favor the CPU-specific version of the assembly (as discussed in Chapter 3, "Shared Assemblies and Strongly Named Assemblies"). However, I can force the CLR to load the IL-neutral version by passing the following string to Assembly's Load method.

```
SomeAssembly, Version=2.0.0.0, Culture=neutral,
PublicKeyToken=01234567890abcde, ProcessorArchitecture=MSIL
```

Today, the CLR supports five possible values for ProcessorArchitecture: MSIL (Microsoft IL), x86, IA64, AMD64, and Arm.

> **Important** Some developers notice that System.AppDomain offers a Load method. Unlike Assembly's static Load method, AppDomain's Load method is an instance method that allows you to load an assembly into the specified AppDomain. This method was designed to be called by unmanaged code, and it allows a host to inject an assembly into a specific AppDomain. Managed code developers generally shouldn't call this method because when AppDomain's Load method is called, you pass it a string that identifies an assembly. The method then applies policy and searches the normal places looking for the assembly. Recall that an AppDomain has settings associated with it that tell the CLR how to look for assemblies. To load this assembly, the CLR will use the settings associated with the specified AppDomain, not the calling AppDomain.
>
> However, AppDomain's Load method returns a reference to an assembly. Because the System.Reflection.Assembly class isn't derived from System.MarshalByRefObject, the assembly object must be marshaled by value back to the calling AppDomain. But the CLR will now use the calling AppDomain's settings to locate the assembly and load it. If the assembly can't be found by using the calling AppDomain's policy and search locations, a FileNotFoundException is thrown. This behavior is usually undesirable and is the reason that you should avoid AppDomain's Load method.

In most dynamically extensible applications, Assembly's Load method is the preferred way of loading an assembly into an AppDomain. However, it does require that you have all of the pieces that make up an assembly's identity. Frequently, developers write tools or utilities (such as ILDasm.exe, PEVerify.exe, CorFlags.exe, GACUtil.exe, SGen.exe, SN.exe, XSD.exe) that perform some kind of processing on an assembly. All of these tools take a command-line argument that refers to the path name of an assembly file (including file extension).
