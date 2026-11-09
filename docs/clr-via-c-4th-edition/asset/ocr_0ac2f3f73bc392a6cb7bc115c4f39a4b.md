# TABLE 2-1 Common Definition Metadata Tables

| Metadata Definition Table Name | Description |
| --- | --- |
| ModuleDef | Always contains one entry that identifies the module. The entry includes the module's file name and extension (without path) and a module version ID (in the form of a GUID created by the compiler). This allows the file to be renamed while keeping a record of its original name. However, renaming a file is strongly discouraged and can prevent the CLR from locating an assembly at run time, so don't do this. |
| TypeDef | Contains one entry for each type defined in the module. Each entry includes the type's name, base type, and flags (public, private, etc.) and contains indexes to the methods it owns in the MethodDef table, the fields it owns in the FieldDef table, the properties it owns in the PropertyDef table, and the events it owns in the EventDef table. |
| MethodDef | Contains one entry for each method defined in the module. Each entry includes the method's name, flags (private, public, virtual, abstract, static, final, etc.), signature, and offset within the module where its IL code can be found. Each entry can also refer to a ParamDef table entry in which more information about the method's parameters can be found. |
| FieldDef | Contains one entry for every field defined in the module. Each entry includes flags (private, public, etc.), type, and name. |
| ParamDef | Contains one entry for each parameter defined in the module. Each entry includes flags (in, out, retval, etc.), type, and name. |
| PropertyDef | Contains one entry for each property defined in the module. Each entry includes flags, type, and name. |
| EventDef | Contains one entry for each event defined in the module. Each entry includes flags and name. |

As the compiler compiles your source code, everything your code defines causes an entry to be created in one of the tables described in Table 2-1. Metadata table entries are also created as the compiler detects the types, fields, methods, properties, and events that the source code references. The metadata created includes a set of reference tables that keep a record of the referenced items. Table 2-2 shows some of the more common reference metadata tables.

# TABLE 2-2 Common Reference Metadata Tables

| Metadata Reference Table Name | Description |
| --- | --- |
| AssemblyRef | Contains one entry for each assembly referenced by the module. Each entry includes the information necessary to bind to the assembly: the assembly's name (without path and extension), version number, culture, and public key token (normally a small hash value generated from the publisher's public key, identifying the referenced assembly's publisher). Each entry also contains some flags and a hash value. This hash value was intended to be a checksum of the referenced assembly's bits. The CLR completely ignores this hash value and will probably continue to do so in the future. |
| ModuleRef | Contains one entry for each PE module that implements types referenced by this module. Each entry includes the module's file name and extension (without path). This table is used to bind to types that are implemented in different modules of the calling assembly's module. |