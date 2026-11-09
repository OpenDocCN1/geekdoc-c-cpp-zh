```
```csharp
// Note: m_value must be read after m_flag is read
if (m_flag == 1)
    Console.WriteLine(m_value);
}
}
```
```

There are some developers (and I am one of them) who do not like C#’s `volatile` keyword, and they think that the language should not provide it.⁶⁹ Our thinking is that most algorithms require few volatile read or write accesses to a field and that most other accesses to the field can occur normally, improving performance; seldom is it required that all accesses to a field be volatile. For example, it is difficult to interpret how to apply volatile read operations to algorithms like this one:

```
```csharp
m_amount = m_amount + m_amount; // Assume m_amount is a volatile field defined in a class
```
```

Normally, an integer number can be doubled simply by shifting all bits left by 1 bit, and many compilers can examine the code above and perform this optimization. However, if `m_amount` is a `volatile` field, then this optimization is not allowed. The compiler must produce code to read `m_amount` into a register and then read it again into another register, add the two registers together, and then write the result back out to the `m_amount` field. The unoptimized code is certainly bigger and slower; it would be unfortunate if it were contained inside a loop.

Furthermore, C# does not support passing a `volatile` field by reference to a method. For example, if `m_amount` is defined as a `volatile Int32`, attempting to call `Int32`’s `TryParse` method causes the compiler to generate a warning as shown here:

```
```csharp
Boolean success = Int32.TryParse("123", out m_amount);
// The above line causes the C# compiler to generate a warning:
// CS0420: a reference to a volatile field will not be treated as volatile
```
```

Finally, volatile fields are not Common Language Specification (CLS) compliant because many languages (including Visual Basic) do not support them.

# Interlocked Constructs

Volatile’s Read method performs an atomic read operation, and its Write method performs an atomic write operation. That is, each method performs either an atomic read operation or an atomic write operation. In this section, we look at the static System.Threading.Interlocked class’ methods. Each of the methods in the Interlocked class performs an atomic read and write operation. In addition, all the Interlocked methods are full memory fences. That is, any variable writes before the call to an Interlocked method execute before the Interlocked method, and any variable reads after the call execute after the call.

The static methods that operate on Int32 variables are by far the most commonly used methods. I show them here:

⁶⁹ By the way, it is good to see that Visual Basic does not offer a volatile semantic built into its language.