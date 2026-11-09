
In most programming scenarios, this silent overflow is undesirable and if not detected causes the application to behave in strange and unusual ways. In some rare programming scenarios (such as calculating a hash value or a checksum), however, this overflow is not only acceptable but is also desired.

Different languages handle overflows in different ways. C and C++ don't consider overflows to be an error and allow the value to wrap; the application continues running. Microsoft Visual Basic, on the other hand, always considers overflows to be errors and throws an exception when it detects one.

The CLR offers IL instructions that allow the compiler to choose the desired behavior. The CLR has an instruction called **add** that adds two values together. The **add** instruction performs no overflow checking. The CLR also has an instruction called **add.ovf** that also adds two values together. However, **add.ovf** throws a **System.OverflowException** if an overflow occurs. In addition to these two IL instructions for the add operation, the CLR also has similar IL instructions for subtraction (**sub/sub.ovf**), multiplication (**mul/mul.ovf**), and data conversions (**conv/conv.ovf**).

C# allows the programmer to decide how overflows should be handled. By default, overflow checking is turned off. This means that the compiler generates IL code by using the versions of the add, subtract, multiply, and conversion instructions that don't include overflow checking. As a result, the code runs faster—but developers must be assured that overflows won't occur or that their code is designed to anticipate these overflows.

One way to get the C# compiler to control overflows is to use the **/checked+** compiler switch. This switch tells the compiler to generate code that has the overflow-checking versions of the add, subtract, multiply, and conversion IL instructions. The code executes a little slower because the CLR is checking these operations to determine whether an overflow occurred. If an overflow occurs, the CLR throws an **OverflowException**.

In addition to having overflow checking turned on or off globally, programmers can control overflow checking in specific regions of their code. C# allows this flexibility by offering **checked** and **unchecked** operators. Here's an example that uses the **unchecked** operator:

```csharp
UInt32 invalid = unchecked((UInt32) (-1));   // OK
```

And here is an example that uses the **checked** operator:

```csharp
Byte b = 100;
b = checked((Byte) (b + 200));      // OverflowException is thrown
```

In this example, **b** and **200** are first converted to 32-bit values and are then added together; the result is 300. Then 300 is converted to a **Byte** due to the explicit cast; this generates the **OverflowException**. If the **Byte** were cast outside the **checked** operator, the exception wouldn't occur:

```csharp
b = (Byte) checked(b + 200);    // b contains 44; no OverflowException
```

In addition to the **checked** and **unchecked** operators, C# also offers **checked** and **unchecked** statements. The statements cause all expressions within a block to be checked or unchecked:

```csharp
checked {                         // Start of checked block
    Byte b = 100;
    b = (Byte) (b + 200);         // This expression is checked for overflow.
}                                 // End of checked block
```

In fact, if you use a **checked** statement block, you can now use the += operator with the **Byte**, which simplifies the code a bit.

```csharp
checked {                // Start of checked block
    Byte b = 100;
    b += 200;            // This expression is checked for overflow.
}                        // End of checked block
```

![](img/3c46ff5b170881db4209d365b1f7a808_136_0.png)

> **Important** Because the only effect that the checked operator and statement has is to determine which versions of the add, subtract, multiply, and data conversion IL instructions are produced, calling a method within a checked operator or statement has no impact on that method, as the following code demonstrates:

```csharp
checked {
    // Assume SomeMethod tries to load 400 into a Byte.
    SomeMethod(400);
    // SomeMethod might or might not throw an OverflowException.
    // It would if SomeMethod were compiled with checked instructions.
}
```

In my experience, I've seen a lot of calculations produce surprising results. Typically, this is due to invalid user input, but it can also be due to values returned from parts of the system that a programmer just doesn't expect. And so, I recommend that programmers do the following:

- Use signed data types (such as **Int32** and **Int64**) instead of unsigned numeric types (such as **UInt32** and **UInt64**) wherever possible. This allows the compiler to detect more overflow/underflow errors. In addition, various parts of the class library (such as **Array's** and **String's** Length properties) are hard-coded to return signed values, and less casting is required as you move these values around in your code. Fewer casts make source code cleaner and easier to maintain. In addition, unsigned numeric types are not CLS-compliant.
- As you write your code, explicitly use **checked** around blocks where an unwanted overflow might occur due to invalid input data, such as processing a request with data supplied from an end user or a client machine. You might want to catch **OverflowException** as well, so that your application can gracefully recover from these failures.
- As you write your code, explicitly use **unchecked** around blocks where an overflow is OK, such as calculating a checksum.
- For any code that doesn't use **checked** or **unchecked**, the assumption is that you *do* want an exception to occur on overflow, for example, calculating something (such as prime numbers) where the inputs are known, and overflows are bugs.

Now, as you develop your application, turn on the compiler's **/checked+** switch for debug builds. Your application will run more slowly because the system will be checking for overflows on any code that you didn't explicitly mark as **checked** or **unchecked**. If an exception occurs, you'll easily detect it and be able to fix the bug in your code. For the release build of your application, use the compiler's **/checked-** switch so that the code runs faster and overflow exceptions won't be generated. To change the Checked setting in Microsoft Visual Studio, display the properties for your project, select the Build tab, click Advanced, and then select the "Check For Arithmetic Overflow/Underflow" option, as shown in Figure 5-1.

If your application can tolerate the slight performance hit of always doing checked operations, then I recommend that you compile with the **/checked** command-line option even for a release build because this can prevent your application from continuing to run with corrupted data and possible security holes. For example, you might perform a multiplication to calculate an index into an array; it is much better to get an **OverflowException** as opposed to accessing an incorrect array element due to the math wrapping around.

![](img/3c46ff5b170881db4209d365b1f7a808_137_0.png)

FIGURE 5-1 Changing the compiler's default setting for performing checked arithmetic using Visual Studio's Advanced Build Settings dialog box

instances don't come under the control of the garbage collector, so their use reduces pressure in the managed heap and reduces the number of collections an application requires over its lifetime.

The .NET Framework SDK documentation clearly indicates which types are reference types and which are value types. When looking up a type in the documentation, any type called a *class* is a reference type. For example, the **System.Exception** class, the **System.IO.FileStream** class, and the **System.Random** class are all reference types. On the other hand, the documentation refers to each value type as a *structure* or an *enumeration*. For example, the **System.Int32** structure, the **System.Boolean** structure, the **System.Decimal** structure, the **System.TimeSpan** structure, the **System.DayOfWeek** enumeration, the **System.IO.FileAttributes** enumeration, and the **System.Drawing.FontStyle** enumeration are all value types.

If you look more closely at the documentation, you'll notice that all of the structures are immediately derived from the **System.ValueType** abstract type. **System.ValueType** is itself immediately derived from the **System.Object** type. By definition, all value types must be derived from **System.ValueType**. All enumerations are derived from the **System.Enum** abstract type, which is itself derived from **System.ValueType**. The CLR and all programming languages give enumerations special treatment. For more information about enumerated types, refer to Chapter 15, "Enumerated Types and Bit Flags."

Even though you can't choose a base type when defining your own value type, a value type can implement one or more interfaces if you choose. In addition, all value types are sealed, which prevents a value type from being used as a base type for any other reference type or value type. So, for example, it's not possible to define any new types using **Boolean**, **Char**, **Int32**, **UInt64**, **Single**, **Double**, **Decimal**, and so on as base types.

> **Important** For many developers (such as unmanaged C/C++ developers), reference types and value types will seem strange at first. In unmanaged C/C++, you declare a type, and then the code that uses the type gets to decide if an instance of the type should be allocated on the thread's stack or in the application's heap. In managed code, the developer defining the type indicates where instances of the type are allocated; the developer using the type has no control over this.

The following code and Figure 5-2 demonstrate how reference types and value types differ:

```csharp
// Reference type (because of 'class')
class SomeRef { public Int32 x; }

// Value type (because of 'struct')
struct SomeVal { public Int32 x; }

static void ValueTypeDemo() {
    SomeRef r1 = new SomeRef();   // Allocated in heap
    SomeVal v1 = new SomeVal();   // Allocated on stack
```
