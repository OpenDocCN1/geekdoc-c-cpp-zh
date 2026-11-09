```
```csharp
public OSVERSIONINFO() {
    OSVersionInfoSize = (UInt32) Marshal.SizeOf(this);
}

public UInt32 OSVersionInfoSize = 0;
public UInt32 MajorVersion      = 0;
public UInt32 MinorVersion      = 0;
public UInt32 BuildNumber       = 0;
public UInt32 PlatformId        = 0;

[MarshalAs(UnmanagedType.ByValTStr, SizeConst = 128)]
public String CSDVersion        = null;
}

internal sealed class MyClass {
    [DllImport("kernel32", CharSet = CharSet.Auto, SetLastError = true)]
    public static extern Boolean GetVersionEx([In, Out] OSVERSIONINFO ver);
}
```
```

In this case, the StructLayout attribute is applied to the OSVERSIONINFO class, the MarshalAs attribute is applied to the CSDVersion field, the DllImport attribute is applied to the GetVersionEx method, and the In and Out attributes are applied to GetVersionEx’s ver parameter. Every programming language defines the syntax a developer must use in order to apply a custom attribute to a target. Microsoft Visual Basic .NET, for example, requires angle brackets (<, >) instead of square brackets.

The CLR allows attributes to be applied to just about anything that can be represented in a file’s metadata. Most commonly, attributes are applied to entries in the following definition tables: TypeDef (classes, structures, enumerations, interfaces, and delegates), MethodDef (including constructors), ParamDef, FieldDef, PropertyDef, EventDef, AssemblyDef, and ModuleDef. Specifically, C# allows you to apply an attribute only to source code that defines any of the following targets: assembly, module, type (class, struct, enum, interface, delegate), field, method (including constructors), method parameter, method return value, property, event, and generic type parameter.

When you’re applying an attribute, C# allows you to specify a prefix specifically indicating the target the attribute applies to. The following code shows all of the possible prefixes. In many cases, if you leave out the prefix, the compiler can still determine the target an attribute applies to, as shown in the previous example. In some cases, the prefix must be specified to make your intentions clear to the compiler. The prefixes shown in italics below are mandatory.

```
```csharp
using System;

[assembly: SomeAttr]             // Applied to assembly
[module:   SomeAttr]             // Applied to module

[type:     SomeAttr]             // Applied to type
internal sealed class SomeType<[typeparam: SomeAttr] T> {  // Applied to generic type variable

    [field: SomeAttr]            // Applied to field
    public Int32 SomeField = 0;
}
```
```