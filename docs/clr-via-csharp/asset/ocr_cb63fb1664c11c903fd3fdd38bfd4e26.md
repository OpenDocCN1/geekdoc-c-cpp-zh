compiler to prefix each type name that appears in source code with the namespace name so that programmers can do less typing.

# ## How Namespaces and Assemblies Relate

Be aware that a namespace and an assembly (the file that implements a type) aren't necessarily related. In particular, the various types belonging to a single namespace might be implemented in multiple assemblies. For example, the `System.IO.FileStream` type is implemented in the `MSCorLib.dll` assembly, and the `System.IO.FileSystemWatcher` type is implemented in the `System.dll` assembly. In fact, the .NET Framework doesn't even ship a `System.IO.dll` assembly.

A single assembly can contain types in different namespaces. For example, the `System.Int32` and `System.Text.StringBuilder` types are both in the `MSCorLib.dll` assembly.

When you look up a type in the .NET Framework SDK documentation, the documentation will clearly indicate the namespace that the type belongs to and also the assembly that the type is implemented in. In Figure 4-1, you can clearly see (right above the Syntax section) that the `ResXFileRef` type is part of the `System.Resources` namespace and that the type is implemented in the `System.Windows.Forms.dll` assembly. To compile code that references the `ResXFileRef` type, you'd add a `using System.Resources;` directive to your source code, and you'd use the `/r:System.Windows.Forms.dll` compiler switch.

![](bbox=[0.2, 0.565, 0.82, 0.855])

**FIGURE 4-1** SDK documentation showing namespace and assembly information for a type