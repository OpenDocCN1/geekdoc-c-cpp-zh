# Windows Executable Files

# Forwarding

As well as being to export functions and values in a module, the export directory
can forward to another library. This allows more flexibility when re-organising
libraries: perhaps some functionality has branched into another module. If so, an export
be forwarded to that library, instead of messy reorganising inside the original module.

Forwarding is achieved by making an RVA in the AddressOfFunctions array point into
t section which contains the export directory, something that normal exports should
dot do. At that location, there should be a zero terminated ASCII string of format
`LibraryName.ExportName` for the appropriate place to forward this to.

# 5.9 Imports

The other half of dynamic linking is importing functions and values into an executable or
other module. Before runtime, compilers and linkers do not know where in memory a value
needs to be imported could exist. The import table solves this by creating an array of
pointers at runtime, each one pointing to the memory location of an imported value. In this way,
ray of pointers exists inside the module at a defined RVA location. In this way, the\linker can use addresses of the module to access values out of.

# 5.9.1 The Import directory

The start of the import directory is pointed to by both the IMAGE_DIRECTORY_
ENTRY_IAT and IMAGE_DIRECTORY_ENTRY_IMPORT entries of the resource di-
rectory (the reason for this is uncertain). At that location, there is an array of IMAGE_\IMPORTDESCRIPTORS structures. Each of these identify a library or module that has
a value we need to import. The array continues until an entry where all the values are
The structure is as follows:

```
struct IMAGE_IMPORT_DESCRIPTOR {
long *OriginalFirstThunk;
long TimeStamp;
long ForwarderChain;
long Name;
long *FirstThunk;
}
```

The TimeStamp is relevant to the act of 'Binding', see below. The Name value is an
RVA to an ASCII string, naming the library to import. ForwarderChain will be explained
later. The only thing of interest at this point, are the RVA's OriginalFirstThunk and
FirstThunk. Both values point to arrays of RVA's, each of which point is equal to
zero. These two arrays are parallel and point to the same structure, in the same order.
reason for this will appear shortly.

Each of these IMAGE_IMPORT_BY_NAMES structs has the following form:

```
struct IMAGE_IMPORT_BY_NAME {
```

50