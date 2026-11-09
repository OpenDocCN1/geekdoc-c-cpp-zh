
executes, the best way for you to load an assembly is to use Assembly's ReflectionOnlyLoadFrom method, or in some rarer cases, Assembly's ReflectionOnlyLoad method. Here are the prototypes of both methods.

```csharp
public class Assembly {
    public static Assembly ReflectionOnlyLoadFrom(String assemblyFile);
    public static Assembly ReflectionOnlyLoad(String assemblyString);
    // Less commonly used overload of ReflectionOnlyLoad is not shown
}
```

The ReflectionOnlyLoadFrom method will load the file specified by the path; the strong-name identity of the file is not obtained, and the file is not searched for in the GAC or elsewhere. The ReflectionOnlyLoad method will search for the specified assembly looking in the GAC, application base directory, private paths, and codebases. However, unlike the Load method, the ReflectionOnlyLoad method does not apply versioning policies, so you will get the exact version that you specify. If you want to apply versioning policy yourself to an assembly identity, you can pass the string into AppDomain's ApplyPolicy method.

When an assembly is loaded with ReflectionOnlyLoadFrom or ReflectionOnlyLoad, the CLR forbids any code in the assembly from executing; any attempt to execute code in an assembly loaded with either of these methods causes the CLR to throw an InvalidOperationException. These methods allow a tool to load an assembly that was delay-signed, would normally require security permissions that prevent it from loading, or was created for a different CPU architecture.

Frequently, when using reflection to analyze an assembly loaded with one of these two methods, the code will have to register a callback method with AppDomain's ReflectionOnlyAssemblyResolve event to manually load any referenced assemblies (calling AppDomain's ApplyPolicy method, if desired); the CLR doesn't do it automatically for you. When the callback method is invoked, it must call Assembly's ReflectionOnlyLoadFrom or ReflectionOnlyLoad method to explicitly load a referenced assembly and return a reference to this assembly.

> **Note** People often ask about assembly unloading. Unfortunately, the CLR doesn't support the ability to unload individual assemblies. If the CLR allowed it, your application would crash if a thread returned back from a method to code in the unloaded assembly. The CLR is all about robustness, security, and allowing an application to crash in this way would be counterproductive to its goals. If you want to unload an assembly, you must unload the entire AppDomain that contains it. This was discussed in great detail in Chapter 22.
>
> It would seem that assemblies loaded with either the ReflectionOnlyLoadFrom or the ReflectionOnlyLoad method could be unloaded. After all, code in these assemblies is not allowed to execute. However, the CLR also doesn't allow assemblies loaded via either of these two methods to be unloaded. The reason is that after an assembly is loaded this way, you can still use reflection to create objects that refer to the metadata defined inside these assemblies. Unloading the assembly would require the objects to be invalidated somehow. Keeping track of this would be too expensive in terms of implementation and execution speed.

Many applications consist of an EXE file that depends on many DLL files. When deploying this application, all the files must be deployed. However, there is a technique that you can use to deploy just a single EXE file. First, identify all the DLL files that your EXE file depends on that do not ship as part of the Microsoft .NET Framework itself. Then add these DLLs to your Visual Studio project. For each DLL file you add, display its properties and change its Build Action to Embedded Resource. This causes the C# compiler to embed the DLL file(s) into your EXE file, and you can deploy this one EXE file.

At run time, the CLR won't be able to find the dependent DLL assemblies, which is a problem. To fix this, when your application initializes, register a callback method with the AppDomain's AssemblyResolve event. The callback method's code should look something like the following:

```csharp
private static Assembly ResolveEventHandler(Object sender, ResolveEventArgs args) {
    String dllName = new AssemblyName(args.Name).Name + ".dll";

    var asm = Assembly.GetExecutingAssembly();
    String resourceName = asm.GetManifestResourceNames().FirstOrDefault(rn =>
rn.EndsWith(dllName));
    if (resourceName == null) return null; // Not found, maybe another handler will find it
    using (var stream = asm.GetManifestResourceStream(resourceName)) {
        Byte[] assemblyData = new Byte[stream.Length];
        stream.Read(assemblyData, 0, assemblyData.Length);
        return Assembly.Load(assemblyData);
    }
}
```

Now, the first time a thread calls a method that references a type in a dependent DLL file, the AssemblyResolve event will be raised and the preceding callback code will find the embedded DLL resource desired and load it by calling an overload of Assembly's Load method that takes a Byte[] as an argument. Although I love the technique of embedding dependent DLLs inside another assembly, you should be aware that this does increase the memory used by your application at run time.

## Using Reflection to Build a Dynamically Extensible Application

As you know, metadata is stored in a bunch of tables. When you build an assembly or a module, the compiler that you're using creates a type definition table, a field definition table, a method definition table, and so on. The System.Reflection namespace contains several types that allow you to write code that reflects over (or parses) these metadata tables. In effect, the types in this namespace offer an object model over the metadata contained in an assembly or a module.

Using these object model types, you can easily enumerate all of the types in a type definition metadata table. Then for each type, you can obtain its base type, the interfaces it implements, and the flags that are associated with the type. Additional types in the System.Reflection namespace allow you to query the type's fields, methods, properties, and events by parsing the corresponding metadata tables. You can also discover any custom attributes (covered in Chapter 18, "Custom Attributes") that have been applied to any of the metadata entities. There are even classes that let you determine referenced assemblies and methods that return the IL byte stream for a method. With all of this information, you could easily build a tool very similar to Microsoft's ILDasm.exe.

```csharp
// Execute this loop once for each Type
// publicly-exported from the loaded assembly
foreach (Type t in a.ExportedTypes) {
    // Display the full name of the type
    Console.WriteLine(t.FullName);
}
}
```

### What Exactly Is a Type Object?

Notice that the previous code iterates over a sequence of System.Type objects. The System.Type type is your starting point for doing type and object manipulations. A System.Type object represents a type reference (as opposed to a type definition).

Recall that System.Object defines a public, nonvirtual instance method named GetType. When you call this method, the CLR determines the specified object's type and returns a reference to its Type object. Because there is only one Type object per type in an AppDomain, you can use equality and inequality operators to see whether two objects are of the same type.

```csharp
private static Boolean AreObjectsTheSameType(Object o1, Object o2) {
    return o1.GetType() == o2.GetType();
}
```

In addition to calling Object's GetType method, the FCL offers several more ways to obtain a Type object:

- The System.Type type offers several overloaded versions of the static GetType method. All versions of this method take a String. The string must specify the full name of the type (including its namespace). Note that the primitive type names supported by the compiler (such as C#'s int, string, bool, and so on) aren't allowed because these names mean nothing to the CLR. If the string is simply the name of a type, the method checks the calling assembly to see whether it defines a type of the specified name. If it does, a reference to the appropriate Type object is returned.

  If the calling assembly doesn't define the specified type, the types defined by MSCorLib.dll are checked. If a type with a matching name still can't be found, null is returned or a System.TypeLoadException is thrown, depending on which overload of the GetType method you called and what parameters you passed to it. The FCL documentation fully explains this method.

  You can pass an assembly-qualified type string, such as "System.Int32, mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089", to GetType. In this case, GetType will look for the type in the specified assembly (loading the assembly if necessary).

- The System.Type type offers a static ReflectionOnlyGetType method. This method behaves similarly to the GetType method mentioned in the previous bullet, except that the type is loaded so that it can be reflected over but cannot be executed.
