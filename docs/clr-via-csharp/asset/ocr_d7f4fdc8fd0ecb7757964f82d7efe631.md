+   - The FCL has many methods that have type names as part of their method names. For example, the **BinaryReader** type offers methods such as **ReadBoolean**, **ReadInt32**, **ReadSingle**, and so on, and the **System.Convert** type offers methods such as **ToBoolean**, **ToInt32**, **ToSingle**, and so on. Although it’s legal to write the following code, the line with **float** feels very unnatural to me, and it’s not obvious that the line is correct:

```
BinaryReader br = new BinaryReader(...);
float val = br.ReadSingle();  // OK, but feels unnatural
Single val = br.ReadSingle();  // OK and feels good
```

+   - Many programmers that use C# exclusively tend to forget that other programming languages can be used against the CLR, and because of this, C#-isms creep into the class library code. For example, Microsoft’s FCL is almost exclusively written in C# and developers on the FCL team have now introduced methods into the library such as **Array’s GetLongLength**, which returns an **Int64** value that is a **long** in C# but not in other languages (like C++/CLI). Another example is **System.Linq.Enumerable’s LongCount** method.

For all of these reasons, I’ll use the FCL type names throughout this book.

In many programming languages, you would expect the following code to compile and execute correctly:

```
Int32  i = 5;   // A 32-bit value
Int64  l = i;   // Implicit cast to a 64-bit value
```

However, based on the casting discussion presented in Chapter 4, you wouldn’t expect this code to compile. After all, **System.Int32** and **System.Int64** are different types, and neither one is derived from the other. Well, you’ll be happy to know that the C# compiler does compile this code correctly, and it runs as expected. Why? The reason is that the C# compiler has intimate knowledge of primitive types and applies its own special rules when compiling the code. In other words, the compiler recognizes common programming patterns and produces the necessary IL to make the written code work as expected. Specifically, the C# compiler supports patterns related to casting, literals, and operators, as shown in the following examples.

First, the compiler is able to perform implicit or explicit casts between primitive types such as these:

```
Int32  i = 5;        // Implicit cast from Int32 to Int32
Int64  l = i;        // Implicit cast from Int32 to Int64
Single s = i;        // Implicit cast from Int32 to Single
Byte   b = (Byte) i; // Explicit cast from Int32 to Byte
Int16  v = (Int16) s; // Explicit cast from Single to Int16
```

C# allows implicit casts if the conversion is “safe,” that is, no loss of data is possible, such as converting an **Int32** to an **Int64**. But C# requires explicit casts if the conversion is potentially