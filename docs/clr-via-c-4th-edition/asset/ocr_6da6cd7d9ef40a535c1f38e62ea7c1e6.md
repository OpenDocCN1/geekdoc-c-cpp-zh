executes, the best way for you to load an assembly is to use Assembly's ReflectionOnlyLoadFrom method, or in some rarer cases, Assembly's ReflectionOnlyLoad method. Here are the prototypes of both methods.

```
```
public class Assembly {
    public static Assembly ReflectionOnlyLoadFrom(String assemblyFile);
    public static Assembly ReflectionOnlyLoad(String assemblyString);
    // Less commonly used overload of ReflectionOnlyLoad is not shown
}
```
```

The ReflectionOnlyLoadFrom method will load the file specified by the path; the strong-name identity of the file is not obtained, and the file is not searched for in the GAC or elsewhere. The ReflectionOnlyLoad method will search for the specified assembly looking in the GAC, application base directory, private paths, and codebases. However, unlike the Load method, the ReflectionOnlyLoad method does not apply versioning policies, so you will get the exact version that you specify. If you want to apply versioning policy yourself to an assembly identity, you can pass the string into AppDomain's ApplyPolicy method.

When an assembly is loaded with ReflectionOnlyLoadFrom or ReflectionOnlyLoad, the CLR forbids any code in the assembly from executing; any attempt to execute code in an assembly loaded with either of these methods causes the CLR to throw an InvalidOperationException. These methods allow a tool to load an assembly that was delay-signed, would normally require security permissions that prevent it from loading, or was created for a different CPU architecture.

Frequently, when using reflection to analyze an assembly loaded with one of these two methods, the code will have to register a callback method with AppDomain's ReflectionOnlyAssemblyResolve event to manually load any referenced assemblies (calling AppDomain's ApplyPolicy method, if desired); the CLR doesn't do it automatically for you. When the callback method is invoked, it must call Assembly's ReflectionOnlyLoadFrom or ReflectionOnlyLoad method to explicitly load a referenced assembly and return a reference to this assembly.

> > **Note** People often ask about assembly unloading. Unfortunately, the CLR doesn't support the ability to unload individual assemblies. If the CLR allowed it, your application would crash if a thread returned back from a method to code in the unloaded assembly. The CLR is all about robustness, security, and allowing an application to crash in this way would be counterproductive to its goals. If you want to unload an assembly, you must unload the entire AppDomain that contains it. This was discussed in great detail in Chapter 22.
> >
> > It would seem that assemblies loaded with either the ReflectionOnlyLoadFrom or the ReflectionOnlyLoad method could be unloaded. After all, code in these assemblies is not allowed to execute. However, the CLR also doesn't allow assemblies loaded via either of these two methods to be unloaded. The reason is that after an assembly is loaded this way, you can still use reflection to create objects that refer to the metadata defined inside these assemblies. Unloading the assembly would require the objects to be invalidated somehow. Keeping track of this would be too expensive in terms of implementation and execution speed.