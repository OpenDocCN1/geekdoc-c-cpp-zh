The first thing you should realize about custom attributes is they're just a way to associate additional information with a target. The compiler emits this additional information into the managed module's metadata. Most attributes have no meaning for the compiler; the compiler simply detects the attributes in the source code and emits the corresponding metadata.

The .NET Framework Class Library (FCL) defines literally hundreds of custom attributes that can be applied to your own source code. Here are some examples:

+   - Applying the DllImport attribute to a method the CLR that the implementation of the method is usually in managed code in the specified DLL
- Applying the Serializable attribute to a type informs the serialization formatters that an instance's fields may be serialized and deserialized.
- Applying the AssemblyVersion attribute to an assembly sets the version number of the assembly.
- Applying the Flags attribute to an enumerated type causes the enumerated type to act as a set of flags.

Following is some C# code with many attributes applied to it. In C#, you apply a custom attribute to a target... wait, let me re-read. Following is some C# code with many attributes applied to it. In C#, you apply a custom attribute to a target by placing the attribute in square brackets immediately before the target. It's not important to understand what this code does. I just want to see what attributes look like.

```
using System;
using System.Runtime.InteropServices;

[StructLayout(Kind.Sequential, CharSet = CharSet.Auto)]
internal sealed class OSVERSIONINFO {
    public OSVersionInfo Size = (UInt32)Marshal.SizeOf(this);

    public UInt32 OSVersionInfo = 0;
    public UInt32 MajorVersion = 0;
    public UInt32 MinorVersion = 0;
    public UInt32 BuildNumber = 0;
    public UInt32 PlatformType = 0;
}

[MarshalAs(UnmanagedType.ByValTStr, SizeConst = 128)]
public string CSDVersion = null;
}

```

```
internal sealed class MyClass {
    [DllImport("Kernel32", CharSet = CharSet.Auto, SetLastError = true)]
    public static extern bool GetVersionEx([In, Out] OSVERSIONINFO ver);
n
```