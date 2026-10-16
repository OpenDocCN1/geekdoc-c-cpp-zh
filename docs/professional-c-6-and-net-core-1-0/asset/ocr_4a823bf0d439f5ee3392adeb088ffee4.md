file? If you are opening an existing file, should any write operations be interpreted as overwriting the contents of the file or appending to the file?

+   3. The *access*, which indicates how you want to access the file. For example, do you want to read from or write to the file or do both?

+   4. The *share* access, which specifies whether you want exclusive access to the file. Alternatively, are you willing to have other streams access the file simultaneously? If so, should other streams have access to read the file, to write to it, or to do both?

The first piece of information is usually represented by a string that contains the full pathname of the file, and this chapter considers only those constructors that require a string here. Besides those, however, some additional constructors take a native Windows handle to a file instead. The remaining three pieces of information are represented by three .NET enumerations called `FileMode`, `FileAccess`, and `FileShare`. The values of these enumerations are listed in the following table and are self-explanatory:

| Enumeration | Values |
|---|---|
| `FileMode` | `Append`, `Create`, `CreateNew`, `Open`, `OpenOrCreate`, or `Truncate` |
| `FileAccess` | `Read`, `ReadWrite`, or `Write` |
| `FileShare` | `Delete`, `Inheritable`, `None`, `Read`, `ReadWrite`, or `Write` |

Note that in the case of `FileMode`, exceptions can be thrown if you request a mode that is inconsistent with the existing status of the file. `Append`, `Open`, and `Truncate` throw an exception if the file does not already exist, and `CreateNew` throws an exception if it does. `Create` and `OpenOrCreate` cope with either scenario, but `Create` deletes any existing file to replace it with a new, initially empty, one. The `FileAccess` and `FileShare` enumerations are bitwise flags, so values can be combined with the C# bitwise or operator, `|`.

# Creating a FileStream

The sample code for StreamSamples makes use of the following dependencies and namespaces:

# Dependencies

```
NETStandard.Library
```

```
System.IO.FileSystem
```

# Namespaces

```
System
```

```
System.Collections.Generic
```

```
System.Globalization
```