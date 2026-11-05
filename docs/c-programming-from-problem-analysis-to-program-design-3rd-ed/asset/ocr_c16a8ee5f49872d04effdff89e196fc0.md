You learned in Chapter 1 that every program must define a `class`. There are thousands of classes that make up the .NET Framework class library. The next section describes some of the predefined data types that are considered primitive data types in most languages. These value and reference types will be explored: `int`, `double`, `decimal`, `bool`, `char`, and `string`.

# Predefined Data Types

The .NET Framework includes a common type system (CTS) that is supported by all .NET languages, including C#. This enables cross-language integration of code—meaning a single application can be written using multiple languages, such as C#, Visual C++, and Visual Basic. The types in the CTS are referred to as common types and are divided into two major categories, as seen in Figure 2-3: value types and reference types.

![](bbox=[0.177, 0.392, 0.688, 0.564])

**Figure 2-3** .NET common types

When placed in memory, value types contain their own copy of data, in binary notation. The data is stored in the actual memory cell that is addressed by the value type’s identifier. In contrast, the contents of reference type memory cells are much different. Reference types contain the address or location in which the sequence of bits is stored. Figure 2-4 shows the difference between how value types are stored and how reference types are stored. An integer value type, such as 2004, representing the year a car was manufactured, is stored directly in the memory cell. To store a string of characters, such as the kind of vehicle, the memory location would contain the address in which “Corvette” is located. The `string` data type is a reference type. The memory location associated with the identifier does not contain the characters “Corvette”, but instead the address in which “Corvette” is stored.