# User-Mode Constructs

The CLR guarantees that and writes to variables of the following data types are atomic: Boolean, Char, (S)Byte, (U)Int16, (U)Int32, (U)IntPtr, Single, and reference types. This means that all bytes within variable are read from or written all at once. So, for example, if you have the following class:

```
internal static class SomeType {
    public static Int32 x = 0;
}
```

and if a thread executes this line of code:

```
SomeType.x = 0x01234567;
```

then the variable will change to 0x00000000 to 0x01234567 all at once (atomically). Another thread cannot possibly see the value in an intermediate state. it is impossible for some other read to query SomeType.x and get a value of 0x01230000. Suppose that the x field in the preceding SomeType class is an Int64. If a thread executes this line of code:

```
SomeType.x = 0x012345678abcdef;
```

it is possible that another thread query x and get a value of 0x0123456700000000 or 0x000000089abcdef, because the read and write operations are not atomic. This is called a torn read.

Although atomic access to variable guarantees that the read or write happens all at once, it does not guarantee when the read or write will happen due to compiler and CPU optimizations. The primitive user-mode constructs discussed in this section are used to enforce the timing of these atomic read and write operations. In addition, these constructs can also force atomic and timed access to variables of additional data types: (U)Int64 and Double.

There are two kinds of primitive user-mode thread synchronization constructs:

+   - Volatile constructs, which perform an atomic read or write operation on a variable containing a simple data type at a specific time
- Interlocked constructs, which perform an atomic read and write operation on a variable containing a simple data type at a specific time

All the volatile and interlocked constructs require you to pass a reference (memory address) to a variable containing a simple data type.

# Volatile Constructs

Back in the early days of computing, software was written using assembly language. Assembly language is so tedious, because programmers must explicitly state everything—use this CPU register for this branch, to that, call indirect through this thing, and so on. To simplify programming,