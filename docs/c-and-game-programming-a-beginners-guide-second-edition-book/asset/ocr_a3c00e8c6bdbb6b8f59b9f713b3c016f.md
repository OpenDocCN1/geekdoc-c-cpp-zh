# Keywords `sizeof` and unsafe

As with C++, C# can use the `sizeof` keyword to gather information pertaining to the size of data types. Unfortunately, this also requires the use of a secondary command, `unsafe`, which is used to mark the unsafe nature of that code. The practicality of using such coding is limited, considering that it takes us out of the .Net environment and puts us back in the archaical world of Windows API. There are, however, legitimate reasons for reverting to that standard; one example is backward compatibility, and another is performance issues. The steps to enable unsafe mode, as well as a simple `sizeof` program, are shown in Example 1.25.

# Example 1.25.  Sizeof and unsafe mode.

```
```csharp
using System;

namespace Chapter1 {
    class Class1 {
        static unsafe void Main() {
            Console.WriteLine("Byte = " + sizeof(byte));
            Console.WriteLine("Sbyte = " + sizeof(sbyte));
            Console.WriteLine("Ushort = " + sizeof(ushort));
            Console.WriteLine("Short = " + sizeof(short));
            Console.WriteLine("Uint = " + sizeof(uint));
            Console.WriteLine("Int = " + sizeof(int));
            Console.WriteLine("Ulong = " + sizeof(ulong));
            Console.WriteLine("Long = " + sizeof(long));
            Console.WriteLine("Float = " + sizeof(float));
            Console.WriteLine("Double = " + sizeof(double));
            Console.WriteLine("Decimal = " + sizeof(decimal));
        }
    }
}
```
```

# Enabling unsafe mode in C#

Once a project is loaded into the .Net compiler, it becomes a simple matter of altering that project’s build configuration to enable unsafe mode.

+   1. From the folder labeled “View,” select the file titled “Solution Explorer” (see Screen Shot 1.7).