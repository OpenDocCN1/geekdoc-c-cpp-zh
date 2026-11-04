# short

The keyword short is a 16-bit integer data type used to store values ranging from -32,768 to 32,767 (see Example B.56).

# Example B.56.

```
```csharp
class Appendix_B {
    static void Main() {
        short Number1 = 1;
    }
}
```
```

# sizeof

The sizeof keyword is used to gather information pertaining to the size of our data types. Unfortunately, this also requires the use of a secondary command, unsafe, which is used to mark the unsafe nature of that code (see Example B.57).

# Example B.57.

```
```csharp
using System;
class Appendix_B {
    static unsafe void Main() {
        Console.WriteLine ("Byte = " + sizeof(byte));
    }
}
```
```

# stackalloc

The keyword stackalloc (stack allocating), is used to allocate blocks of memory referenced from a stack. The addresses of these blocks are stored as pointers and they are protected from garbage collection, thus they do not have to be fixed/pinned. Note: All blocks are lost when their methods are terminated (see Example B.58).

# Example B.58.

```
```csharp
class Appendix_B {
    public static unsafe void Main() {
        int* pointer1 = stackalloc int[3];
        pointer1[0] = 1;
    }
}
```
```