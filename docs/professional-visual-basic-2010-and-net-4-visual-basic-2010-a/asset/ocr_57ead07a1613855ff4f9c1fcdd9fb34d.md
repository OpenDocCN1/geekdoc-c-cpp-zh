Unfortunately, in the past developers had a tendency to tell the system to interpret a variable created as a Boolean as an Integer. This is referred to as implicit conversion and is related to Option Strict. It is not the best practice, and when .NET was introduced, it caused issues for Visual Basic because the underlying representation of True in other languages wasn’t going to match those of Visual Basic. The result was that Visual Basic represents True differently for implicit conversions than other .NET languages.

True has been implemented in such a way that when converted to an integer, Visual Basic converts a value of True to -1 (negative one). This is one of the few (but not the only) legacy carryovers from older versions of Visual Basic, and is different from other languages, which typically use the integer value 1. Generically, all languages tend to implicitly convert False to 0, and True to a nonzero value.

However, Visual Basic works as part of a multilingual environment, with metadata-defining interfaces, so the external value of True is as important as its internal value. Fortunately, Microsoft implemented Visual Basic in such a way that while -1 is supported, the .NET standard of 1 is exposed from Visual Basic methods to other languages.

To create reusable code, it is always better to avoid implicit conversions. In the case of Booleans, if the code needs to check for an integer value, then you should explicitly evaluate the Boolean and create an appropriate integer. The code will be far more maintainable and prone to fewer unexpected results.

# Integer Types

Now that Booleans have been covered in depth, the next step is to examine the Integer types that are part of Visual Basic. Visual Basic 6.0 included two types of integer values: The Integer type was limited to a maximum value of 32767, and the Long type supported a maximum value of 2147483647.

The .NET Framework added a new integer type, the Short. The Short is the equivalent of the Integer value from Visual Basic 6.0; the Integer has been promoted to support the range previously supported by the Visual Basic 6.0 Long type, and the Visual Basic .NET Long type is an eight-byte value. The new Long type provides support for 64-bit values, such as those used by current 64-bit processors. In addition, each of these types also has two alternative types. In all, Visual Basic supports the nine Integer types described in Table 2-2.

TABLE 2-2: Visual Basic Integer Types

| TYPE | ALLOCATED MEMORY | MINIMUM VALUE | MAXIMUM VALUE |
| Short | 2 bytes | -32768 | 32767 |
| Int16 | 2 bytes | -32768 | 32767 |
| UInt16 | 2 bytes | 0 | 65535 |
| Integer | 4 bytes | -2147483648 | 2147483647 |
| Int32 | 4 bytes | -2147483648 | 2147483647 |
| UInt32 | 4 bytes | 0 | 4294967295 |
| Long | 8 bytes | -9223372036854775808 | 9223372036854775807 |
| Int64 | 8 bytes | -9223372036854775808 | 9223372036854775807 |
| UInt64 | 8 bytes | 0 | 18446744073709551615 |

# Short

A Short value is limited to the maximum value that can be stored in two bytes. This means there are 16 bits and the value can range between -32768 and 32767. This limitation may or may not be based on the amount of memory physically associated with the value; it is a definition of what must occur in the .NET Framework. This is important, because there is no guarantee that the implementation will actually use less memory than when using an Integer value. It is possible that in order to optimize memory or processing,