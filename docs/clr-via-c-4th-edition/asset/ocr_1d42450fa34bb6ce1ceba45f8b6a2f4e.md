In many programming languages, you would expect the following code to compile and execute correctly.

```
```csharp
Int32 i = 5;      // A 32-bit value
Int64 l = i;      // Implicit cast to a 64-bit value
```
```

However, based on the casting discussion presented in Chapter 4, you wouldn't expect this code to compile. After all, System.Int32 and System.Int64 are different types, and neither one is derived from the other. Well, you'll be happy to know that the C# compiler does compile this code correctly, and it runs as expected. Why? The reason is that the C# compiler has intimate knowledge of primitive types and applies its own special rules when compiling the code. In other words, the compiler recognizes common programming patterns and produces the necessary IL to make the written code work as expected. Specifically, the C# compiler supports patterns related to casting, literals, and operators, as shown in the following examples.

First, the compiler is able to perform implicit or explicit casts between primitive types such as the following.

```
```csharp
Int32  i = 5;       // Implicit cast from Int32 to Int32
Int64  l = i;       // Implicit cast from Int32 to Int64
Single s = i;       // Implicit cast from Int32 to Single
Byte   b = (Byte) i; // Explicit cast from Int32 to Byte
Int16  v = (Int16) s; // Explicit cast from Single to Int16
```
```

C# allows implicit casts if the conversion is "safe," that is, no loss of data is possible, such as converting an Int32 to an Int64. But C# requires explicit casts if the conversion is potentially unsafe. For numeric types, "unsafe" means that you could lose precision or magnitude as a result of the conversion. For example, converting from Int32 to Byte requires an explicit cast because precision might be lost from large Int32 numbers; converting from Single to Int16 requires a cast because Single can represent numbers of a larger magnitude than Int16 can.

Be aware that different compilers can generate different code to handle these cast operations. For example, when casting a Single with a value of 6.8 to an Int32, some compilers could generate code to put a 6 in the Int32, and others could perform the cast by rounding the result up to 7. By the way, C# always truncates the result. For the exact rules that C# follows for casting primitive types, see the "Conversions" section in the C# language specification.

In addition to casting, primitive types can be written as literals. A literal is considered to be an instance of the type itself, and therefore, you can call instance methods by using the instance as shown here.

```
```csharp
Console.WriteLine(123.ToString() + 456.ToString());   // "123456"
```
```

Also, if you have an expression consisting of literals, the compiler is able to evaluate the expression at compile time, improving the application's performance.

```
```csharp
Boolean found = false;      // Generated code sets found to 0
Int32 x = 100 + 20 + 3;     // Generated code sets x to 123
String s = "a " + "bc";     // Generated code sets s to "a bc"
```
```