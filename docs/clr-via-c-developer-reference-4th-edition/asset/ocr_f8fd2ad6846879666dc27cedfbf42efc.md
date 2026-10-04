Of course, for desktop applications, the old API still exists so that it doesn't break existing code when re-compiling. However, the new API is the recommended API going forward, and that is why I explain the new API exclusively in this chapter. For Windows Store Apps (where backward compatibility is not an issue), using the new API is mandatory.

# Assembly Loading

As you know, the just-in-time (JIT) compiler compiles the Intermediate Language (IL) for a method, it sees what types are referenced in the IL code. Then at run, the JIT compiler uses the assembly's TypeRef and AssemblyRef metadata tables to determine what assembly defines the type being referenced. The AssemblyRef metadata table contains all of the parts that make up the strong name of the assembly.—name (without extension or path), version, culture, and public key token—concatenates them into a string, and then attempts to load an assembly this identity into the AppDomain (assuming it's not already loaded). If the assembly being loaded weakly named, the identity is the name of the assembly (no version, culture, or public key token information).

Internally, the CLR attempts to load this assembly using the System.Reflection.Assembly class's static Load method. This method is publicly documented, and you can call it to explicitly load an assembly into your AppDomain. This method is the CLR equivalent of Win32.LoadLibrary function. There are actually several overloaded versions of Assembly's Load method. Here are the more commonly used overloaded versions.

```
public class Assembly {
public static Assembly Load(AssemblyName assemblyRef);
public static Assembly Load(String assemblyString);
// Less commonly used overloads of Load are not shown
}
```

Internally, Load calls the CLR to apply a version-binding redirection policy to the assembly and looks for the assembly in the global assembly cache (GAC), following by the application's base directory, private subdirectories, and codebase locations. If you call Load by passing a weakly named assembly, Load doesn't apply a version-binding redirection policy to the assembly, and the CLR won't look in the GAC for the assembly. If Load finds the specified assembly, it returns a reference to an Assembly object that represents the loaded assembly. If Load fails to find the specified assembly, it throws a System.FileNotFoundException.

584 PART IV Core Facilities