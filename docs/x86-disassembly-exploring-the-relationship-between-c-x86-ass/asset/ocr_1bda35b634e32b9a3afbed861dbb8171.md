# Imports

short Hint;
char Name(ASCII);

'Name' is an ASCII string of any size that names the value to be imported. This is used when looking up a value in an export directory (see above) through the AddressOfNames array. The 'Hint' is an index into the AddressOfNames array; save searching for a string, the loader first checks the AddressOfNames entry corresponding to 'Hint'.

To summarise: The import table consists of a large array of IMAGE_IMPORT_DESCRIPTORs, terminated by an all-zero entry. These descriptors identify a library to import things. From there are two parallel arrays, each pointing to IMAGE_IMPORT_BY_NAME structures, which identify a specific value to be imported.

# 5.9.2 Imports at runtime

Using the above import directory at runtime, the loader finds the appropriate modules, loads them into memory, seeks the correct export. However, to use the export, a pointer to it must be stored somewhere in the importing module's memory. This is why there are two parallel arrays, OriginalFirstThunk and FirstThunk, identifying IMAGE_IMPORT_BY_NAME structures. Once an imported value has been resolved, the pointer to it is stored in the FirstThunk array. It can then be used at runtime to address imported values.

# 5.9.3 Bound imports

The PE format also supports a peculiar feature known as 'binding'. In the process of loading and resolving import addresses can be time consuming, and in situations this is to be avoided. If a developer is fairly certain that a library is not going to be updated or changed, the addresses in memory of imported values will not change each time the application is loaded. So, the import can be computed and stored in the FirstThunk array before runtime, allowing the loader to skip resolving the imports - the imports are 'bound' to a particular memory location. However, if the versions numbers between modules do out of date, or the imported library needs to be relocated, the loader will assume the bound addresses are invalid, and resolve the imports.

The Timestamp member of the import directory entry for a module controls binding; if it is set to zero, the import is not bound. If it is non-zero, then it is bound to another module. However, the Timestamp in the import table must match the Timestamp in the module's Header, otherwise the bound values will be discarded by the loader.

# Forwarding and binding

Binding can of course be a problem if the bound library / module forwards its exports to another module. In these cases, the non-forwarded imports can be bound, but the values which get forwarded must be identified so the loader can resolve them. This is done through the ForwarderChain member of the import descriptor. The value of "ForwarderChain" is an

51