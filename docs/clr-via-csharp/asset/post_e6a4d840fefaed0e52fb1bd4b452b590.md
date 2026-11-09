
This is a very powerful feature that should be used with extreme caution because it allows you to perform direct memory accesses. If these memory accesses are outside the bounds of the array, an exception will not be thrown; instead, you will be corrupting memory, violating type safety, and possibly opening a security hole! For this reason, the assembly containing the unsafe code must either be granted full trust or at least have the Security Permission with Skip Verification turned on.

The following C# code demonstrates three techniques (safe, jagged, and unsafe), for accessing a two-dimensional array:

```csharp
using System;
using System.Diagnostics;

public static class Program {
    private const Int32 c_numElements = 10000;

    public static void Main() {
        const Int32 testCount = 10;
        Stopwatch sw;

        // Declare a two-dimensional array
        Int32[,] a2Dim = new Int32[c_numElements, c_numElements];

        // Declare a two-dimensional array as a jagged array (a vector of vectors)
        Int32[][] aJagged = new Int32[c_numElements][];
        for (Int32 x = 0; x < c_numElements; x++)
            aJagged[x] = new Int32[c_numElements];

        // 1: Access all elements of the array using the usual, safe technique
        sw = Stopwatch.StartNew();
        for (Int32 test = 0; test < testCount; test++)
            Safe2DimArrayAccess(a2Dim);
        Console.WriteLine("{0}: Safe2DimArrayAccess", sw.Elapsed);

        // 2: Access all elements of the array using the jagged array technique
        sw = Stopwatch.StartNew();
        for (Int32 test = 0; test < testCount; test++)
            SafeJaggedArrayAccess(aJagged);
        Console.WriteLine("{0}: SafeJaggedArrayAccess", sw.Elapsed);

        // 3: Access all elements of the array using the unsafe technique
        sw = Stopwatch.StartNew();
        for (Int32 test = 0; test < testCount; test++)
            Unsafe2DimArrayAccess(a2Dim);
        Console.WriteLine("{0}: Unsafe2DimArrayAccess", sw.Elapsed);
        Console.ReadLine();
    }

    private static Int32 Safe2DimArrayAccess(Int32[,] a) {
        Int32 sum = 0;
        for (Int32 x = 0; x < c_numElements; x++) {
            for (Int32 y = 0; y < c_numElements; y++) {
                sum += a[x, y];
            }
        }
        return sum;
    }

    private static Int32 SafeJaggedArrayAccess(Int32[][] a) {
        Int32 sum = 0;
        for (Int32 x = 0; x < c_numElements; x++) {
            for (Int32 y = 0; y < c_numElements; y++) {
                sum += a[x][y];
            }
        }
        return sum;
    }

    private static unsafe Int32 Unsafe2DimArrayAccess(Int32[,] a) {
        Int32 sum = 0;
        fixed (Int32* pi = a) {
            for (Int32 x = 0; x < c_numElements; x++) {
                Int32 baseOfDim = x * c_numElements;
                for (Int32 y = 0; y < c_numElements; y++) {
                    sum += pi[baseOfDim + y];
                }
            }
        }
        return sum;
    }
}
```

The **Unsafe2DimArrayAccess** method is marked with the **unsafe** modifier, which is required to use C#'s **fixed** statement. To compile this code, you'll have to specify the **/unsafe** switch when invoking the C# compiler or check the "**Allow Unsafe Code**" check box on the Build tab of the Project Properties pane in Microsoft Visual Studio.

When I run this program on my machine, I get the following output:

```
00:00:02.0017692: Safe2DimArrayAccess
00:00:01.5197844: SafeJaggedArrayAccess
00:00:01.7343436: Unsafe2DimArrayAccess
```

As you can see, the safe two-dimensional array access technique is the slowest. The safe jagged array access technique takes a little less time to complete than the safe two-dimensional array access technique. However, you should note that creating the jagged array is more time-consuming than creating the multi-dimensional array because creating the jagged array requires an object to be allocated on the heap for each dimension, causing the garbage collector to kick in periodically. So there is a trade-off. If you need to create a lot of "multi-dimensional arrays" and you intend to access the elements infrequently, it is quicker to create a multi-dimensional array. If you need to create the "multi-dimensional array" just once, and you access its elements frequently, a jagged array will give you better performance. Certainly, in most applications, the latter scenario is more common.

```csharp
using System;

public static class Program {
    public static void Main() {
        StackallocDemo();
        InlineArrayDemo();
    }

    private static void StackallocDemo() {
        unsafe {
            const Int32 width = 20;
            Char* pc = stackalloc Char[width]; // Allocates array on stack

            String s = "Jeffrey Richter";    // 15 characters

            for (Int32 index = 0; index < width; index++) {
                pc[width - index - 1] =
                    (index < s.Length) ? s[index] : '.';
            }

            // The line below displays "....................rethciR yerffeJ"
            Console.WriteLine(new String(pc, 0, width));
        }
    }

    private static void InlineArrayDemo() {
        unsafe {
            CharArray ca;                           // Allocates array on stack
            Int32 widthInBytes = sizeof(CharArray);
            Int32 width = widthInBytes / 2;

            String s = "Jeffrey Richter"; // 15 characters

            for (Int32 index = 0; index < width; index++) {
                ca.Characters[width - index - 1] =
                    (index < s.Length) ? s[index] : '.';
            }

            // The line below displays "....................rethciR yerffeJ"
            Console.WriteLine(new String(ca.Characters, 0, width));
        }
    }
}

internal unsafe struct CharArray {
    // This array is embedded inline inside the structure
    public fixed Char Characters[20];
}
```

Normally, because arrays are reference types, an array field defined in a structure is really just a pointer or reference to an array; the array itself lives outside of the structure’s memory. However, it is possible to embed an array directly inside a structure as shown by the CharArray structure in the preceding code. To embed an array directly inside a structure, there are several requirements:

- The type must be a structure (value type); you cannot embed an array inside a class (reference type).
- The field or its defining structure must be marked with the **unsafe** keyword.
- The array field must be marked with the **fixed** keyword.
- The array must be single-dimensional and zero-based.
- The array’s element type must be one of the following types: **Boolean, Char, SByte, Byte, Int32, UInt32, Int64, UInt64, Single,** or **Double**.

Inline arrays are typically used for scenarios that involve interoperating with unmanaged code where the unmanaged data structure also has an inline array. However, inline arrays can be used in other scenarios as well. The **InlineArrayDemo** method in the code shown earlier offers an example of how to use an inline array. The **InlineArrayDemo** method performs the same function as the **StackallocDemo** method; it just does it in a different way.

## Chapter 17 Delegates

**In this chapter:**

- A First Look at Delegates ................................................ 405
- Using Delegates to Call Back Static Methods ............................... 408
- Using Delegates to Call Back Instance Methods ............................ 409
- Demystifying Delegates ................................................... 410
- Using Delegates to Call Back Many Methods (Chaining) ..................... 415
- Enough with the Delegate Definitions Already (Generic Delegates) ........ 422
- C#’s Syntactical Sugar for Delegates .................................... 423
- Delegates and Reflection ................................................. 431

In this chapter, I talk about callback functions. Callback functions are an extremely useful programming mechanism that has been around for years. The Microsoft .NET Framework exposes a callback function mechanism by using delegates. Unlike callback mechanisms used in other platforms, such as unmanaged C++, delegates offer much more functionality. For example, delegates ensure that the callback method is type-safe, in keeping with one of the most important goals of the common language runtime (CLR). Delegates also integrate the ability to call multiple methods sequentially and support the calling of static methods as well as instance methods.

### A First Look at Delegates

The C runtime’s qsort function takes a pointer to a callback function to sort elements within an array. In Microsoft Windows, callback functions are required for window procedures, hook procedures, asynchronous procedure calls, and more. In the .NET Framework, callback methods are used for a whole slew of things. For example, you can register callback methods to get a variety of notifications such as unhandled exceptions, window state changes, menu item selections, file system changes, form control events, and completed asynchronous operations.

In unmanaged C/C++, the address of a non-member function is just a memory address. This address doesn’t carry any additional information such as the number of parameters the function expects, the types of these parameters, the function’s return value type, and the function’s calling convention. In short, unmanaged C/C++ callback functions are not type-safe (although they are a very lightweight mechanism).
