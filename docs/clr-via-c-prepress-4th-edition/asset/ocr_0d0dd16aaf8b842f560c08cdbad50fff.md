# A Brief Look at Metadata

Now we know what kind of PE file we've created. But what exactly is in the Program.exe file? A managed PE file has four main parts: the PE32(+) header, the CLR header, the metadata, and the IL. The PE32(+) header is the standard information that Windows expects. The CLR header is a small block of information that is specific to modules that require the CLR (managed modules). The header includes the major and minor version number of the CLR that the module was built for; some flags, a MethodDef token (described later) indicating the module's entry point method if this module is a CUI, GUI or Windows Store executable, and an optional strong-name digital signature (discussed in Chapter 3). Finally, the header contains the size and offsets of certain metadata tables contained within the module. You can see the exact format of the CLR header by examining the IMAGE_COR20_HEADER defined in the CorHdr.h header file.

The metadata is a block of binary data that consists of several tables. There are three categories of tables: definition tables, reference tables, and manifest tables. Table 2-1 describes some of the more common definition tables that exist in a module's metadata block.

TABLE 2-1 Common Definition Metadata Tables

| Metadata Definition Table Name | Description |
| --- | --- |
| ModuleDef | Always contains one entry that identifies the module. The entry includes the module's file name and extension (without path) and a module version ID (in the form of a GUID created by the compiler). This allows the file to be renamed while keeping a record of its original name. However, renaming a file is strongly discouraged and can prevent the CLR from locating an assembly at runtime, so don't do this. |
| TypeDef | Contains one entry for each type defined in the module. Each entry includes the type's name, base type, and flags (public, private, etc.) and contains indexes to the methods it owns in the MethodDef table, the fields it owns in the FieldDef table, the properties it owns in the PropertyDef table, and the events it owns in the EventDef table. |
| MethodDef | Contains one entry for each method defined in the module. Each entry includes the method's name, flags (private, public, virtual, abstract, static, final, etc.), signature, and offset within the module where its IL code can be found. Each entry can also refer to a ParamDef table entry in which more information about the method's parameters can be found. |
| FieldDef | Contains one entry for every field defined in the module. Each entry includes flags (private, public, etc.), type, and name. |
| ParamDef | Contains one entry for each parameter defined in the module. Each entry includes flags (in, out, retval, etc.), type, and name. |