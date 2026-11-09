
Chapter 3, “Shared Assemblies and Strongly Named Assemblies”. However, I can force the CLR to load the IL-neutral version by passing the following string to Assembly’s Load method:

```text
"SomeAssembly, Version=2.0.0.0, Culture=neutral,
PublicKeyToken=01234567890abcde, ProcessorArchitecture=MSIL"
```

Today, the CLR supports five possible values for ProcessorArchitecture: MSIL (Microsoft IL), x86, IA64, AMD64, and ARM.

**Important** Some developers notice that System.AppDomain offers a Load method. Unlike Assembly’s static Load method, AppDomain’s Load method is an instance method that allows you to load an assembly into the specified AppDomain. This method was designed to be called by unmanaged code, and it allows a host to inject an assembly into a specific AppDomain. Managed code developers generally shouldn’t call this method because when AppDomain’s Load method is called, you pass it a string that identifies an assembly. The method then applies policy and searches the normal places looking for the assembly. Recall that an AppDomain has settings associated with it that tell the CLR how to look for assemblies. To load this assembly, the CLR will use the settings associated with the specified AppDomain, not the calling AppDomain.

However, AppDomain’s Load method returns a reference to an assembly. Because the System.Reflection.Assembly class isn’t derived from System.MarshalByRefObject, the assembly object must be marshaled by value back to the calling AppDomain. But the CLR will now use the calling AppDomain’s settings to locate the assembly and load it. If the assembly can’t be found using the calling AppDomain’s policy and search locations, a FileNotFoundException is thrown. This behavior is usually undesirable and is the reason that you should avoid AppDomain’s Load method.

In most dynamically extensible applications, Assembly’s Load method is the preferred way of loading an assembly into an AppDomain. However, it does require that you have all of the pieces that make up an assembly’s identity. Frequently, developers write tools or utilities (such as ILDasm.exe, PEVerify.exe, CorFlags.exe, GACUtil.exe, SGen.exe, SN.exe, XSD.exe) that perform some kind of processing on an assembly. All of these tools take a command-line argument that refers to the path name of an assembly file (including file extension). To load an assembly specifying a path name, you call Assembly’s LoadFrom method:

```csharp
public class Assembly {
    public static Assembly LoadFrom(String path);
    // Less commonly used overloads of LoadFrom are not shown
}
```

Internally, LoadFrom first calls System.Reflection.AssemblyName’s static GetAssemblyName method, which opens the specified file, finds the AssemblyDef metadata table’s entry, and extracts the assembly identity information and returns it in a System.Reflection.AssemblyName object (the file is also closed). Then, LoadFrom internally calls Assembly’s Load method, passing it the AssemblyName object. At this point, the CLR applies a version-binding redirection policy and searches the various locations looking for a matching assembly. If Load finds the assembly, it will load it, and an Assembly object that represents the loaded assembly will be returned; LoadFrom returns this value. If Load fails to find an assembly, LoadFrom loads the assembly at the path name specified in LoadFrom’s argument. Of course, if an assembly with the same identity is already loaded, LoadFrom simply returns an Assembly object that represents the already loaded assembly.

By the way, the LoadFrom method allows you to pass a URL as the argument. Here is an example:

```csharp
Assembly a = Assembly.LoadFrom(@"http://www.wintellect.com/SomeAssembly.dll");
```

When you pass an Internet location, the CLR downloads the file, installs it into the user's download cache, and loads the file from there. Note that you must be online or an exception will be thrown. However, if the file has been downloaded previously, and if Windows Internet Explorer has been set to work offline (see Internet Explorer's Work Offline menu item in its File menu), the previously downloaded file will be used, and no exception will be thrown. You can also call UnsafeLoadFrom, which can load a web-downloaded assembly, bypassing some security checks.

**Important** It is possible to have different assemblies on a single machine all with the same identity. Because LoadFrom calls Load internally, it is possible that the CLR will not load the specified file and instead will load a different file giving you unexpected behavior. It is highly recommended that each build of your assembly change the version number; this ensures that each version has its own identity, and because of this, LoadFrom will now work as expected.

Microsoft Visual Studio's UI designers and other tools typically use Assembly's LoadFile method. This method can load an assembly from any path and can be used to load an assembly with the same identity multiple times into a single AppDomain. This can happen as changes to an application's UI are made in the designer/tool and the user rebuilds the assembly. When loading an assembly via LoadFile, the CLR will not resolve any dependencies automatically; your code must register with AppDomain's AssemblyResolve event and have your event callback method explicitly load any dependent assemblies.

If you are building a tool that simply analyzes an assembly's metadata via reflection (as discussed later in this chapter), and you want to ensure that none of the code contained inside the assembly executes, the best way for you to load an assembly is to use Assembly's ReflectionOnlyLoadFrom method, or in some rarer cases, Assembly's ReflectionOnlyLoad method. Here are the prototypes of both methods:

```csharp
public class Assembly {
   public static Assembly ReflectionOnlyLoadFrom(String assemblyFile);
   public static Assembly ReflectionOnlyLoad(String assemblyString);
   // Less commonly used overload of ReflectionOnlyLoad is not shown
}
```

The ReflectionOnlyLoadFrom method will load the file specified by the path; the strong-name identity of the file is not obtained, and the file is not searched for in the GAC or elsewhere. The ReflectionOnlyLoad method will search for the specified assembly looking in the GAC, application base directory, private paths, and codebases. However, unlike the Load method, the ReflectionOnlyLoad method does not apply versioning policies, so you will get the exact version that you specify. If you want to apply versioning policy yourself to an assembly identity, you can pass the string into AppDomain's ApplyPolicy method.

When an assembly is loaded with ReflectionOnlyLoadFrom or ReflectionOnlyLoad, the CLR forbids any code in the assembly from executing; any attempt to execute code in an assembly loaded with either of these methods causes the CLR to throw an InvalidOperationException. These methods allow a tool to load an assembly that was delay-signed, would normally require security permissions that prevent it from loading, or was created for a different CPU architecture.

Frequently when using reflection to analyze an assembly loaded with one of these two methods, the code will have to register a callback method with AppDomain's ReflectionOnlyAssemblyResolve event to manually load any referenced assemblies (calling AppDomain's ApplyPolicy method, if desired); the CLR doesn't do it automatically for you. When the callback method is invoked, it must call Assembly's ReflectionOnlyLoadFrom or ReflectionOnlyLoad method to explicitly load a referenced assembly and return a reference to this assembly.

**Note** People often ask about assembly unloading. Unfortunately, the CLR doesn't support the ability to unload individual assemblies. If the CLR allowed it, your application would crash if a thread returned back from a method to code in the unloaded assembly. The CLR is all about robustness, security, and allowing an application to crash in this way would be counterproductive to its goals. If you want to unload an assembly, you must unload the entire AppDomain that contains it. This was discussed in great detail in Chapter 22.

It would seem that assemblies loaded with either the ReflectionOnlyLoadFrom or the ReflectionOnlyLoad method could be unloaded. After all, code in these assemblies is not allowed to execute. However, the CLR also doesn't allow assemblies loaded via either of these two methods to be unloaded. The reason is that once an assembly is loaded this way, you can still use reflection to create objects that refer to the metadata defined inside these assemblies. Unloading the assembly would require the objects to be invalidated somehow. Keeping track of this would be too expensive in terms of implementation and execution speed.

Many applications consist of an EXE file that depends on many DLL files. When deploying this application, all the files must be deployed. However, there is a technique that you can use to deploy just a single EXE file. First, identify all the DLL files that your EXE file depends on that do not ship as part of the Microsoft .NET Framework itself. Then add these DLLs to your Visual Studio project. For each DLL file you add, display its properties and change its "Build Action" to "Embedded Resource". This causes the C# compiler to embed the DLL file(s) into your EXE file, and you can deploy this one EXE file.

At runtime, the CLR won't be able to find the dependent DLL assemblies, which is a problem. To fix this, when your application initializes, register a callback method with the AppDomain's AssemblyResolve event. The callback method's code should look something like this:

```csharp
private static Assembly ResolveEventHandler(Object sender, ResolveEventArgs args) {
    String dllName = new AssemblyName(args.Name).Name + ".dll";

    var assem = Assembly.GetExecutingAssembly();
    String resourceName = assem.GetManifestResourceNames().FirstOrDefault(rn => rn.EndsWith(dllName));
```
