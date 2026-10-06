# 5.8 Exports

Exports are functions and values in one module to be shared with other modules. This is done through the use of the "Export Directory", which is used to translate the name of an export (or "Ordinal", see below), and a location in memory where the code or data can be found. The start of the export directory is identified by the IMAGE_DIRECTORY_ENTRY entry of the resource directory. All export data must exist in the same section. The directory is headed by the following structure:

```
struct IMAGE_EXPORT_DIRECTORY {
    long Characteristics;
    long TimeStamp;
    short MajorVersion;
    short MinorVersion;
    long Name;
    long Base;
    long NumberOfFunctions;
    long *AddressOfFunctions;
    long *AddressOfNames;
    long *AddressOfOrdinals;
}
```

The 'Characteristics' value is generally unused, TimeStamp describes the time the export was generated, MajorVersion and MinorVersion describe the version details of the directory, but their nature is undefined. These values have little or no impact on the actual exports themselves. The 'Name' value is an RVA to a zero terminated ASCII string, the name of this library name, or module.

# Names and Ordinals

Each export has both a name and an 'ordinal' (a kind of index). The actual exports themselves are described through AddressOfFunctions, which is an RVA to an array of RVAs, each pointing to a function or value to be exported. The size of this array is in the value NumberOfFunctions. Each of these functions has an ordinal. The 'Base' value is used as the ordinal of the first export, and the next RVA in the array is Base+1, and so.

Each entry in AddressOfFunctions is identified by a name, found through the RVA AddressOfNames. The data where AddressOfNames points to an array of RVAs, each RVA points to a zero terminated ASCII string, each being the name of an export. There is also a second array, pointed to by the RVA in AddressNameOrdinals. This is also of size NumberOfNames, but each value is a 16 bit word, each being an ordinal. These two arrays are parallel and are used to get an export value from AddressOfFunctions. To find an export by name, search the AddressOfNames array for the correct string and then take the corresponding ordinal from the AddressNameOrdinals array. This ordinal is then used to get an index to a value in AddressOfFunctions.