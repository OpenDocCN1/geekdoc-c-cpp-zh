
the IL source code files. ILAsm.exe will produce a single file containing all of the types. This technique requires your source code compiler to produce IL-only code.

**Important** To summarize, an assembly is a unit of reuse, versioning, and security. It allows you to partition your types and resources into separate files so that you, and consumers of your assembly, get to determine which files to package together and deploy. Once the CLR loads the file containing the manifest, it can determine which of the assembly's other files contain the types and resources the application is referencing. Anyone consuming the assembly is required to know only the name of the file containing the manifest; the file partitioning is then abstracted away from the consumer and can change in the future without breaking the application's behavior.

If you have multiple types that can share a single version number and security settings, it is recommended that you place all of the types in a single file rather than spread the types out over separate files, let alone separate assemblies. The reason is performance. Loading a file/assembly takes the CLR and Windows time to find the assembly, load it, and initialize it. The fewer files/assemblies loaded the better, because loading fewer assemblies helps reduce working set and also reduces fragmentation of a process's address space. Finally, NGen.exe can perform better optimizations when processing larger files.

To build an assembly, you must select one of your PE files to be the keeper of the manifest. Or you can create a separate PE file that contains nothing but the manifest. Table 2-3 shows the manifest metadata tables that turn a managed module into an assembly.

## TABLE 2-3 Manifest Metadata Tables

| Manifest Metadata Table Name | Description |
|---|---|
| AssemblyDef | Contains a single entry if this module identifies an assembly. The entry includes the assembly's name (without path and extension), version (major, minor, build, and revision), culture, flags, hash algorithm, and the publisher's public key (which can be null). |
| FileDef | Contains one entry for each PE and resource file that is part of the assembly (except the file containing the manifest since it appears as the single entry in the AssemblyDef table). The entry includes the file's name and extension (without path), hash value, and flags. If this assembly consists only of its own file, the FileDef table has no entries. |
| ManifestResourceDef | Contains one entry for each resource that is part of the assembly. The entry includes the resource's name, flags (public if visible outside the assembly and private otherwise), and an index into the FileDef table indicating the file that contains the resource file or stream. If the resource isn't a stand-alone file (such as .jpg or a .gif), the resource is a stream contained within a PE file. For an embedded resource, the entry also includes an offset indicating the start of the resource stream within the PE file. |
| ExportedTypesDef | Contains one entry for each public type exported from all of the assembly's PE modules. The entry includes the type's name, an index into the FileDef table (indicating which of this assembly's files implements the type), and an index into the TypeDef table. Note: To save file space, types exported from the file containing the manifest are not repeated in this table because the type information is available using the metadata's TypeDef table. |

The existence of a manifest provides a level of indirection between consumers of the assembly and the partitioning details of the assembly and makes assemblies self-describing. Also, note that the file containing the manifest has metadata information that indicates which files are part of the assembly, but the individual files themselves do not have metadata information that specifies that they are part of the assembly.

**Note** The assembly file that contains the manifest also has an AssemblyRef table in it. This table contains an entry for all of the assemblies referenced by all of the assembly's files. This allows tools to open an assembly's manifest and see its set of referenced assemblies without having to open the assembly's other files. Again, the entries in the AssemblyRef table exist to make an assembly self-describing.

The C# compiler produces an assembly when you specify any of the following command-line switches: /t[arget]:exe, /t[arget]:winexe, /t[arget]:appcontainerexe, /t[arget]:library, or /t[arget]:winmdobj. All of these switches cause the compiler to generate a single PE file that contains the manifest metadata tables. The resulting file is either a CUI executable, a GUI executable, a Windows Store executable, a class library, or a WINMD library respectively.

In addition to these switches, the C# compiler supports the /t[arget]:module switch. This switch tells the compiler to produce a PE file that doesn't contain the manifest metadata tables. The PE file produced is always a DLL PE file, and this file must be added to an assembly before the CLR can access any types within it. When you use the /t:module switch, the C# compiler, by default, names the output file with an extension of .netmodule.

**Important** Unfortunately, the Microsoft Visual Studio integrated development environment (IDE) doesn't natively support the ability for you to create multifile assemblies. If you want to create multifile assemblies, you must resort to using command-line tools.

There are many ways to add a module to an assembly. If you're using the C# compiler to build a PE file with a manifest, you can use the /addmodule switch. To understand how to build a multifile assembly, let’s assume that we have two source code files:

² When using /t[arget]:winmdobj, the resulting .winmdobj file must be passed to the WinMDExp.exe tool, which massages the metadata a bit in order to expose the assembly's public CLR types as Windows Runtime types. The WinMDExp.exe tool does not touch the IL code in any way.

- RUT.cs, which contains rarely used types
- FUT.cs, which contains frequently used types

Let’s compile the rarely used types into their own module so that users of the assembly won’t need to deploy this module if they never access the rarely used types:

```
csc /t:module RUT.cs
```

This line causes the C# compiler to create a RUT.netmodule file. This file is a standard DLL PE file, but, by itself, the CLR can’t load it.

Next let’s compile the frequently used types into their own module. We’ll make this module the keeper of the assembly’s manifest because the types are used so often. In fact, because this module will now represent the entire assembly, I’ll change the name of the output file to MultiFileLibrary.dll instead of calling it FUT.dll:

```
csc /out:MultiFileLibrary.dll /t:library /addmodule:RUT.netmodule FUT.cs
```

This line tells the C# compiler to compile the FUT.cs file to produce the MultiFileLibrary.dll file. Because /t:library is specified, a DLL PE file containing the manifest metadata tables is emitted into the MultiFileLibrary.dll file. The /addmodule:RUT.netmodule switch tells the compiler that RUT.netmodule is a file that should be considered part of the assembly. Specifically, the /addmodule switch tells the compiler to add the file to the FileDef manifest metadata table and to add RUT.netmodule’s publicly exported types to the ExportedTypesDef manifest metadata table.

Once the compiler has finished all of its processing, the two files shown in Figure 2-1 are created. The module on the right contains the manifest.

![](img/3f2c86949cdef7e2f9e27c37c607b28e_51_0.png)

**FIGURE 2-1** A multifile assembly consisting of two managed modules, one with a manifest.

The RUT.netmodule file contains the IL code generated by compiling RUT.cs. This file also contains metadata tables that describe the types, methods, fields, properties, events, and so on that are defined by RUT.cs. The metadata tables also describe the types, methods, and so on that are referenced by RUT.cs. The MultiFileLibrary.dll is a separate file. Like RUT.netmodule, this file includes the IL code generated by compiling FUT.cs and also includes similar definition and reference metadata tables. However, MultiFileLibrary.dll contains the additional manifest metadata tables, making MultiFileLibrary.dll an assembly. The additional manifest metadata tables describe all of the files that make up the assembly (the MultiFileLibrary.dll file itself and the RUT.netmodule file). The manifest metadata tables also include all of the public types exported from MultiFileLibrary.dll and RUT.netmodule.

> **Note** In reality, the manifest metadata tables don’t actually include the types that are exported from the PE file that contains the manifest. The purpose of this optimization is to reduce the number of bytes required by the manifest information in the PE file. So statements like “The manifest metadata tables also include all the public types exported from MultiFileLibrary.dll and RUT.netmodule” aren’t 100 percent accurate. However, this statement does accurately reflect what the manifest is logically exposing.

Once the MultiFileLibrary.dll assembly is built, you can use ILDasm.exe to examine the metadata’s manifest tables to verify that the assembly file does in fact have references to the RUT.netmodule file’s types. Here is what the FileDef and ExportedTypesDef metadata tables look like:

```
File #1 (26000001)
---------------------------------------------
    Token: 0x26000001
    Name : RUT.netmodule
    HashValue Blob : e6 ed 6f 62 2c a1 2c 59 97 65 0f 21 44 10 15 96 f2 7e db c2
    Flags : [ContainsMetaData]  (00000000)

ExportedType #1 (27000001)
---------------------------------------------
    Token: 0x27000001
    Name: ARarelyUsedType
    Implementation token: 0x26000001
    TypeDef token: 0x02000002
    Flags     : [Public] [AutoLayout] [Class] [Sealed] [AnsiClass]
                [BeforeFieldInit] (00100101)
```

From this, you can see that RUT.netmodule is a file considered to be part of the assembly with the token 0x26000001. From the ExportedTypesDef table, you can see that there is a publicly exported type, ARarelyUsedType. The implementation token for this type is 0x26000001, which indicates that the type’s IL code is contained in the RUT.netmodule file.

> **Note** For the curious, metadata tokens are 4-byte values. The high byte indicates the type of token (0x01=TypeRef, 0x02=TypeDef, 0x23=AssemblyRef, 0x26=File (file definition), 0x27=ExportedType). For the complete list, see the CorTokenType enumerated type in the CorHdr.h file included with the .NET Framework SDK. The three lower bytes of the token simply identify the row in the corresponding
