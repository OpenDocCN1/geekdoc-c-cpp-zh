
that the operator is defined within. The reason for this restriction is that it enables the C# compiler to search for a possible method to bind to in a reasonable amount of time.

Here is an example of an operator overload method defined in a C# class definition.

```csharp
public sealed class Complex {
    public static Complex operator+(Complex c1, Complex c2) { ... }
}
```

The compiler enters a metadata definition for an entry called _Add; the method entry also has the special flag set, indicating that this is a "special" method. When language compilers (including the C# compiler) see a + operator specified in source code, they look to see if one of the operand's types defines a specialname _Add whose parameters are compatible with the operand's types. If this method exists, the compiler emits code to this method. If no method exists, a compilation error occurs.

Tables 8-1 and 8-2 show the set of unary and binary operators that C# supports being overloaded, their symbols, and the corresponding Common Language Specification (CLS) method name that the compiler emits. I explain the three columns in the next section.

## TABLE 8-1 C Unary Operators and Their CLS-Compliant Method Names

| C Operator Symbol | Special Method Name | Suggested CLS-Compliant Method Name |
|---|---|---|
| + | op_UnaryPlus | Plus |
| - | op_UnaryNegation | Negate |
| ! | op_LogicalNot | Not |
| ~ | op_OnesComplement | OnesComplement |
| ++ | op_Increment | Increment |
| -- | op_Decrement | Decrement |
| (none) | op_True | IsTrue { get; } |
| (none) | op_False | IsFalse { get; } |

## TABLE 8-2 C Binary Operators and Their CLS-Compliant Method Names

| C Operator Symbol | Special Method Name | Suggested CLS-Compliant Method Name |
|---|---|---|
| + | op_Addition | Add |
| - | op_Subtraction | Subtract |
| * | op_Multiply | Multiply |
| / | op_Division | Divide |
| % | op_Modulus | Mod |
| & | op_BitwiseAnd | BitwiseAnd |
| | | op_BitwiseOr | BitwiseOr |
| ^ | op_ExclusiveOr | Xor |
| << | op_LeftShift | LeftShift |
| >> | op_RightShift | RightShift |
| == | op_Equality | Equals |
| != | op_Inequality | Equals |
| < | op_LessThan | Compare |
| > | op_GreaterThan | Compare |
| <= | op_LessThanOrEqual | Compare |
| >= | op_GreaterThanOrEqual | Compare |

The CLR specification defines many additional operators that can be overloaded, but C# does not support these additional operators. Therefore, they are not in mainstream use, so I will not list them. If you are interested in the complete list, please see the ECMA specifications (www.ecma-international.org/publications/standards/Ecma-335.html) for the Common Language Infrastructure (CLI), Partition I, Concepts and Architecture, Sections 10.3.1 (unary operators) and 10.3.2 (binary operators).

> If you examine the core numeric types (Int32, Int64, UInt32) in the Framework Class Library (FCL), you'll see they don't define any operator methods. The reason they don't is that compilers specify for operations on these primitive types and emit IL instructions that directly manipulate instances of these types. If the types were to offer methods and compilers were to emit code to call these methods, a run-time performance cost would be associated with the method call. Plus, the method would ultimately have to execute some IL instructions to perform the expected operation anyway. This is the reason why the FCL types don't define any operator overload methods. Here's what this means to you: if the programming language you're using doesn't support one of the core FCL types, you won't be able to perform any operations on instances of that type.

## Operators and Programming Language Interoperability

Operator overloading can be a very useful tool, allowing developers to express their thoughts with succinct code. However, not all programming languages support operator overloading. When using a language that doesn't support operator overloading, the language will know how to interpret the + operator (unless the type is a primitive in that language), and the compiler will emit an error. When using languages that do not support operator overloading, the language would allow you to call the desired op_ directly (such as op_Addition).

If you are using a language that doesn't support + operator overloading to be defined in a type, obviously, this type could still offer an op_Addition method. From C#, expect that you could call this op_Addition method by using the + operator, but you cannot. When the C# compiler detects it, it looks for an op_Addition method that has the special metadata flag associated with it so that the compiler knows for sure the op_Addition method is intended to be an operator overload. Because the op_Addition method is produced by a language that doesn't support overloads, the method won't have the special flag associated with it, and the C# compiler will produce a compilation error. Of course, in any language you explicitly call a method that happens to be named op_Addition, but the compilers won't translate a usage of the + symbol to call this method.

## Jeff's Opinion About Microsoft's Operator Name Rules

I'm sure that all of these rules about when you can't call an operator overload method seem very confusing and complicated. If compilers that supported operator overloading didn't emit the special metadata flag, the rules would be a lot simpler, and programmers would have an easier time working with that operator overload methods. Languages that support operator overloading would support the operator symbol syntax, and all languages would support calling the various op methods explicitly. I can come up with any reason why Microsoft made this so difficult, and I hope they'll loosen these rules in future versions of their compilers.

For a type that defines operator methods, Microsoft recommends that you define friendlier public static methods that call the operator overload internally. For example, a public-friendly named method Complex Add should be defined by a type that overloads the op_Add method. The third column in Tables 8-1 and 8-2 lists the recommended friendly name for each operator. So the Complex type shown earlier should be defined in the following way.

```csharp
public sealed class Complex {
    public static Complex operator+(Complex c1, Complex c2) { ... }
    public static Complex Add(Complex c1, Complex c2) { ... }
}
```

## Conversion Operator Methods

Occasionally, you need to convert an object from one type to a different type. For example, I'm sure you've had to convert a Byte to Int32 at some point. When the source type and target type are a primitive, the compiler knows how to emit the necessary code (cast). If the source type or target type is not a primitive, the CLR checks if the source object is the same as the target type. For example, the System.Xml.Linq class allows you to convert an Extensible Markup Language (XML) element to a Boolean, Int32, Int64, Single, Double, Decimal, String, DateTime, TimeSpan, Guid, or the null equivalent of any of these types. You could also imagine that the FCL included a Rational type that might be convenient to convert an Int32 or a Single object to a Rational object. Moreover, it might also be nice to

To make these conversions, the Rational type should define public constructors that take a single parameter: an instance of the type you're converting. You should also define public instance methods that take parameters (like the very popular ToString method). Each method will convert an instance of the defining type to the target type.

```csharp
public sealed class Rational {
    // Constructs a Rational from an Int32
    public Rational(Int32 num) { ... }

    // Constructs a Rational from a Single
    public Rational(Single num) { ... }

    // Converts a Rational to an Int32
    public Int32 ToInt32() { ... }

    // Converts a Rational to a Single
    public Single ToSingle() { ... }
}
```
