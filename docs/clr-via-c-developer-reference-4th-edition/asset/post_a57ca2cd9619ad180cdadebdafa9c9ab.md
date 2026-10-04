
I've identified three reasons to use multifile assemblies:

- You can partition your types among separate files, allowing for files to be incrementally downloaded as described in the Internet download scenario. Partitioning the types into separate files also allows for partial or piecemeal packaging and deployment for applications you purchase and install.

- You can add resource or data files to your assembly. For example, you could have a type that calculates some information. This type might require access to some metadata tables. Instead of embedding the metadata tables in your source code, you could use a tool (such as AssemblyLinker) so that the file is considered to be part of your assembly. By the way, this data can be in any format—a text file, a spreadsheet, or whatever you like—as long as your assembly knows how to parse the contents.

- You can create assemblies combining types from different programming languages. For example, you can implement some types in C#, some types in Visual Basic, and other types in other languages. When you compile types with C#, the compiler produces a module. When you compile other types with Visual Basic, the compiler produces a module. You can then use a tool to combine all of these modules into a single assembly.

**Important**: To summarize, an assembly is a unit of reuse, versioning, and security. It allows you to partition your types and resources into separate files so that consumers of your assembly determine which files to package and deploy. After the CLR loads the file containing the manifest, it can determine the assembly's behavior. If you have multiple types that can share a single version number and security settings, it is recommended that you place all of the types in a single file rather than spread the types over separate assemblies. The reason is performance. Loading a file/assembly takes the CLR to find, load, and initialize it. The fewer assemblies loaded the better, because it helps working set and also reduces fragmentation. Finally, NGen.exe can perform better optimizations when processing larger files.

To build an assembly, you must select one of your files to be the keeper of the manifest. You can create a separate PE file that contains nothing but the manifest. Table 2-3 shows the metadata tables that turn a managed module into an assembly.

### TABLE 2-3 Manifest Metadata Tables

| Table Name | Description |
| :--- | :--- |
| AssemblyDef | Contains a single entry if this module identifies the assembly. The entry includes the assembly name (without path and extension), version (major, minor, and revision), culture, flags, and publisher key (which can be null). |
| FileDef | Contains one entry for each PE and resource file that is part of the assembly (except the file containing the manifest as it appears in the AssemblyDef table). The entry includes the file's name, relative path, and flags. This assembly consists only of its own file, which has no entries. |
| ResourceDef | Contains one entry for each resource that is part of the assembly. The entry includes the resource's name, type (public if visible outside assembly or otherwise), and an index into the FileDef table. If the resource is a standalone file (such as a .jpg or .gif), the resource is a stream contained within a file. The entry also includes an offset indicating the stream within the file. |
| ExportTypesDef | Contains one entry for each public type exported from the assembly's PE modules. The entry includes the type's name, an index into the FileDef (indicating which of this assembly's files it implements), and an index into the TypeDef table. Note: To save file space, types exported from the file containing the manifest are not repeated in this table because the type information is available using the manifest's TypeDef. |

The existence of a manifest provides a level of indirection between consumers of the assembly and the partitioning details of the assembly and makes assemblies self-describing. Also, note that the file containing the manifest metadata indicates which files are part of the assembly, but the individual files themselves do not have metadata that they are part of the assembly.

**Note**: The assembly file that contains the manifest also has an AssemblyRef table. This table contains an entry for all of the assemblies referenced by the assembly. This allows tools to open an assembly's manifest and see its set of referenced assemblies without having to open other files. Again, the entries in the AssemblyRef table exist to make an assembly self-describing.

The C# compiler produces an assembly when you specify any of the following command-line switches: /target:exe, /target:winexe, /target:library, or /target:winmdobj;¹ All of these switches cause the compiler to generate a single PE file that contains the manifest metadata tables. The resulting file is a CLI executable, a GUI executable, a Windows Store executable, a class library, or a WINMD library respectively.

¹ When using /target:winmdobj, the resulting winmdobj file must be passed to the WINMDExp.exe tool, which massages the metadata in order to expose the assembly's public CLR types as Windows types. The WINMDExp.exe tool does not touch the IL code in any way

In addition to switches, the C# compiler supports the /target:module switch. This switch tells the compiler to produce a PE file that doesn't contain the metadata tables. The PE file produced is always a DLL file, and this file must be added to an assembly before the CLR can access types within it. When you use the /t:module switch, the C# compiler, by default, names the output file with an extension of .netmodule

> **Unfortunately**, the Microsoft Visual Studio integrated development environment (IDE) doesn't natively support the ability to create multifile assemblies. If you want to create multifile assemblies, you must resort to using command-line tools.

There are many ways to add a module to an assembly. If you're using the C# compiler to build a PE file with a manifest, you can use the /module switch. To understand how to build a multifile assembly, let's assume that we have two source code files:

- RUT.cs, which contains rarely used types
- FUT.cs, which contains frequently used types

Let's compile the rarely used into their own module so that users of the assembly won't need to deploy this module if they never access the used types.

```
csc /t:module RUT.cs
```

This line causes the C# compiler to create a RUT.netmodule file. This file is a standard DLL file, but by itself, the CLR can't load it.

Next let's compile the frequently used into their own module. We'll make this module the keeper of the assembly's manifest because the types are so often. In fact, because this module will now represent the entire assembly, I'll change the name of the output file to MultiFileLibrary.dll instead of RUT.dll.

```
csc /out:MultiFileLibrary.dll /t:library /addmodule:RUT.netmodule FUT.cs
```

This line tells the C# compiler to compile the FUT.cs to produce the MultiFileLibrary.dll because /t:library is specified, a DLL file containing the manifest tables is emitted into the MultiFileLibrary.dll file. The /module:RUT.netmodule switch tells the compiler that RUT.netmodule is a file that should be considered part of the assembly. Specifically, the /module switch tells the compiler to add the FileDef metadata table and to add RUT.module's exported types to the ExportedTypes own metadata table.
