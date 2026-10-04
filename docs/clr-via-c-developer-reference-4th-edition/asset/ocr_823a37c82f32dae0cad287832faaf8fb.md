To build an assembly, you must select one of your PE files to be the keeper of the manifest. You can create a separate PE file that contains nothing but the manifest. Table 2-3 shows the manifest metadata tables that turn a managed module into an assembly.

# TABLE 2-3 Manifest Metadata Tables

| Manifest Table Name | Description |
|---|---|
| AssemblyDef | Contains a single entry if this module identifies the assembly. The entry includes the assembly name (without path and extension), version (major, minor, bound, and revision), culture, flags, hash algorithm, and publisher key (which can be null). |
| FileDef | Contains one entry for each PE and resource file that is part of the assembly (except the file containing the manifest as it appears in the AssemblyDef table). The entry includes the file's name, relative path, hash, and flags. This assembly consists only of its own file, the FileDef has no entries. |
| ResourceDef | Contains one entry for each resource that is part of the assembly. The entry includes the resource's name, type (public if visible outside assembly or otherwise), and an index into the FileDef table that contains the resource or stream. If the resource is a stand-alone file (such as a .jpg or a .gif), the resource is a stream contained within a file. The entry also includes an offset indicating the stream within the file |
| ExportTypesDef | Contains one entry for each public type exported from all of the assembly's PE modules. The entry includes the type's name, an index into the FileDef (indicating which of this assembly's files it implements), and an index into the TypeDef table. Note: To save file space, types exported from the file containing the manifest are not repeated in this table because the type information is available using the manifest's TypeDef.

The existence of a manifest provides a level of indirection between consumers of the assembly and the partitioning details of the assembly and makes assemblies self-describing. Also, note that the file containing the manifest metadata indicates which files are part of the assembly, but the individual files themselves do not have metadata information that they are part of the assembly.

> Note The assembly file that contains the manifest also has an AssemblyRef table. This table contains an entry for all of the assemblies referenced by all of the assemblies. This allows tools to open an assembly's manifest and see its set of referenced assemblies without having to open the assembly's other files. Again, the entries in the AssemblyRef table exist to make an assembly self-describing.

The C# compiler produces an assembly when you specify any of the following command-line switches: /t[arget]:exe, /t[arget]:winex, /t[arget]:cominteraxerse, /t[arget]:library, or /t[arget]:winmdobj;¹ All of these switches cause the compiler to generate a single PE file that contains the manifest metadata tables. The resulting file is a CUI executable, a GUI executable, a Windows Store executable, a class library, or a WINMD library respectively.

¹ When using /t[arget]:winmdobj, the resulting winmdobj file must be passed to the WINMDExp.exe tool, which massages the metadata in bit order to expose the assembly's public CLR types as Windows types. The WINMDExp.exe tool does not touch the IL code in any