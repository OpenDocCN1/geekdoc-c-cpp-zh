> **Important** It is possible to have different assemblies on a single machine all with the same identity. Because **LoadFrom** calls **Load** internally, it is possible that the CLR will not load the specified file and instead will load a different file giving you unexpected behavior. It is highly recommended that each build of your assembly change the version number; this ensures that each version has its own identity, and because of this, **LoadFrom** will now work as expected.

Microsoft Visual Studio's UI designers and other tools typically use **Assembly's LoadFile** method. This method can load an assembly from any path and can be used to load an assembly with the same identity multiple times into a single AppDomain. This can happen as changes to an application's UI are made in the designer/tool and the user rebuilds the assembly. When loading an assembly via **LoadFile**, the CLR will not resolve any dependencies automatically; your code must register with **AppDomain's AssemblyResolve** event and have your event callback method explicitly load any dependent assemblies.

If you are building a tool that simply analyzes an assembly's metadata via reflection (as discussed later in this chapter), and you want to ensure that none of the code contained inside the assembly executes, the best way for you to load an assembly is to use **Assembly's ReflectionOnlyLoadFrom** method, or in some rarer cases, **Assembly's ReflectionOnlyLoad** method. Here are the prototypes of both methods:

```
```
public class Assembly {
    public static Assembly ReflectionOnlyLoadFrom(String assemblyFile);
    public static Assembly ReflectionOnlyLoad(String assemblyString);
    // Less commonly used overload of ReflectionOnlyLoad is not shown
}
```
```

The **ReflectionOnlyLoadFrom** method will load the file specified by the path; the strong-name identity of the file is not obtained, and the file is not searched for in the GAC or elsewhere. The **ReflectionOnlyLoad** method will search for the specified assembly looking in the GAC, application base directory, private paths, and codebases. However, unlike the **Load** method, the **ReflectionOnlyLoad** method does not apply versioning policies, so you will get the exact version that you specify. If you want to apply versioning policy yourself to an assembly identity, you can pass the string into **AppDomain's ApplyPolicy** method.

When an assembly is loaded with **ReflectionOnlyLoadFrom** or **ReflectionOnlyLoad**, the CLR forbids any code in the assembly from executing; any attempt to execute code in an assembly loaded with either of these methods causes the CLR to throw an **InvalidOperationException**. These methods allow a tool to load an assembly that was delay-signed, would normally require security permissions that prevent it from loading, or was created for a different CPU architecture.

Frequently when using reflection to analyze an assembly loaded with one of these two methods, the code will have to register a callback method with **AppDomain's ReflectionOnlyAssemblyResolve** event to manually load any referenced assemblies