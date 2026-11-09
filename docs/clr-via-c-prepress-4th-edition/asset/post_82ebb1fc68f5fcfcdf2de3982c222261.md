
conversion. For example, converting from `Int32` to `Byte` requires an explicit cast because precision might be lost from large `Int32` numbers; converting from `Single` to `Int16` requires a cast because `Single` can represent numbers of a larger magnitude than `Int16` can.

Be aware that different compilers can generate different code to handle these cast operations. For example, when casting a `Single` with a value of 6.8 to an `Int32`, some compilers could generate code to put a 6 in the `Int32`, and others could perform the cast by rounding the result up to 7. By the way, C# always truncates the result. For the exact rules that C# follows for casting primitive types, see the “Conversions” section in the C# language specification.

In addition to casting, primitive types can be written as literals. A literal is considered to be an instance of the type itself, and therefore, you can call instance methods by using the instance as shown here:

```csharp
Console.WriteLine(123.ToString() + 456.ToString());  // "123456"
```

Also, if you have an expression consisting of literals, the compiler is able to evaluate the expression at compile time, improving the application’s performance.

```csharp
Boolean found = false;       // Generated code sets found to 0
Int32 x = 100 + 20 + 3;     // Generated code sets x to 123
String s = "a" + "b";       // Generated code sets s to "ab"
```

Finally, the compiler automatically knows how and in what order to interpret operators (such as +, -, *, /, %, &, ^, |, ==, !=, >, <, >=, <=, <<, >>, ~, !, ++, --, and so on) when used in code:

```csharp
Int32 x = 100;              // Assignment operator
Int32 y = x + 23;           // Addition and assignment operators
Boolean lessThanFifty = (y < 50);  // Less-than and assignment operators
```

## Checked and Unchecked Primitive Type Operations

Programmers are well aware that many arithmetic operations on primitives could result in an overflow:

```csharp
Byte b = 100;
b = (Byte) (b + 200);       // b now contains 44 (or 2C in Hex).
```

**Important** When performing the arithmetic operation above, the first step requires that all operand values be expanded to 32-bit values (or 64-bit values if any operand requires more than 32 bits). So b and 200 (values requiring less than 32 bits) are first converted to 32-bit values and then added together. The result is a 32-bit value (300 in decimal, or 12C in hexadecimal) that must be cast to a Byte before the result can be stored back in the variable b. C# doesn’t perform this cast for you implicitly, which is why the Byte cast on the second line of the preceding code is required.

In most programming scenarios, this silent overflow is undesirable and if not detected causes the application to behave in strange and unusual ways. In some rare programming scenarios (such as calculating a hash value or a checksum), however, this overflow is not only acceptable but is also desired.

Different languages handle overflows in different ways. C and C++ don't consider overflows to be an error and allow the value to wrap; the application continues running. Microsoft Visual Basic, on the other hand, always considers overflows to be errors and throws an exception when it detects one.

The CLR offers IL instructions that allow the compiler to choose the desired behavior. The CLR has an instruction called add that adds two values together. The add instruction performs no overflow checking. The CLR also has an instruction called add.ovf that also adds two values together. However, add.ovf throws a System.OverflowException if an overflow occurs. In addition to these two IL instructions for the add operation, the CLR also has similar IL instructions for subtraction (sub/sub.ovf), multiplication (mul/mul.ovf), and data conversions (conv/conv.ovf).

C# allows the programmer to decide how overflows should be handled. By default, overflow checking is turned off. This means that the compiler generates IL code by using the versions of the add, subtract, multiply, and conversion instructions that don't include overflow checking. As a result, the code runs faster—but developers must be assured that overflows won't occur or that their code is designed to anticipate these overflows.

One way to get the C# compiler to control overflows is to use the /checked+ compiler switch. This switch tells the compiler to generate code that has the overflow-checking versions of the add, subtract, multiply, and conversion IL instructions. The code executes a little slower because the CLR is checking these operations to determine whether an overflow occurred. If an overflow occurs, the CLR throws an OverflowException.

In addition to having overflow checking turned on or off globally, programmers can control overflow checking in specific regions of their code. C# allows this flexibility by offering checked and unchecked operators. Here's an example that uses the unchecked operator:

```csharp
UInt32 invalid = unchecked((UInt32) (-1));   // OK
```

And here is an example that uses the checked operator:

```csharp
Byte b = 100;
b = checked((Byte) (b + 200));      // OverflowException is thrown
```

In this example, b and 200 are first converted to 32-bit values and are then added together; the result is 300. Then 300 is converted to a Byte due to the explicit cast; this generates the OverflowException. If the Byte were cast outside the checked operator, the exception wouldn't occur.

```csharp
b = (Byte) checked(b + 200);       // b contains 44; no OverflowException
```

In addition to the checked and unchecked operators, C# also offers checked and unchecked statements. The statements cause all expressions within a block to be checked or unchecked:

```csharp
checked {
    Byte b = 100;                         // Start of checked block
    b = (Byte) (b + 200);                 // This expression is checked for overflow.
}                                         // End of checked block
```

In fact, if you use a checked statement block, you can now use the += operator with the Byte, which simplifies the code a bit:

```csharp
checked {           // Start of checked block
    Byte b = 100;
    b += 200;        // This expression is checked for overflow.
}                   // End of checked block
```

**Important** Because the only effect that the checked operator and statement have is to determine which versions of the add, subtract, multiply, and data conversion IL instructions are produced, calling a method within a checked operator or statement has no impact on that method, as the following code demonstrates:

```csharp
checked {
    // Assume SomeMethod tries to load 400 into a Byte.
    SomeMethod(400);
    // SomeMethod might or might not throw an OverflowException.
    // It would if SomeMethod were compiled with checked instructions.
}
```

In my experience, I've seen a lot of calculations produce surprising results. Typically, this is due to invalid user input, but it can also be due to values returned from parts of the system that a programmer just doesn't expect. And so, I now recommend that programmers do the following:

- Use signed data types (such as Int32 and Int64) instead of unsigned numeric types (such as UInt32 and UInt64) wherever possible. This allows the compiler to detect more overflow/underflow errors. In addition, various parts of the class library (such as Array's and String's Length properties) are hard-coded to return signed values, and less casting is required as you move these values around in your code. Fewer casts make source code cleaner and easier to maintain. In addition, unsigned numeric types are not CLS-compliant.
- As you write your code, explicitly use checked around blocks where an unwanted overflow might occur due to invalid input data, such as processing a request with data supplied from an end user or a client machine. You might want to catch OverflowException as well, so that your application can gracefully recover from these failures.
- As you write your code, explicitly use unchecked around blocks where an overflow is OK, such as calculating a checksum.
- For any code that doesn't use checked or unchecked, the assumption is that you do want an exception to occur on overflow, for example, calculating something (such as prime numbers) where the inputs are known, and overflows are bugs.

Now, as you develop your application, turn on the compiler's /checked+ switch for debug builds. Your application will run more slowly because the system will be checking for overflows on any code that you didn't explicitly mark as checked or unchecked. If an exception occurs, you'll easily detect it and be able to fix the bug in your code. For the release build of your application, use the compiler's /checked- switch so that the code runs faster and overflow exceptions won't be generated. To change
