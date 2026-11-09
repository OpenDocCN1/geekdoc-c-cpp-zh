and then write the result back out to the m_amount field. The unoptimized code is certainly bigger and slower; it would be unfortunate if it were contained inside a loop.

Furthermore, C# does not support passing a volatile field by reference to a method. For example, if m_amount is defined as a volatile Int32, attempting to call Int32's TryParse method causes the compiler to generate a warning as shown here.

```
~~~csharp
Boolean success = Int32.TryParse("123", out m_amount);
// The preceding line causes the C# compiler to generate a warning:
// CS0420: a reference to a volatile field will not be treated as volatile
~~~
```

Finally, volatile fields are not Common Language Specification (CLS) compliant because many languages (including Visual Basic) do not support them.

# ## Interlocked Constructs

Volatile's Read method performs an atomic read operation, and its Write method performs an atomic write operation. That is, each method performs either an atomic read operation or an atomic write operation. In this section, we look at the static System.Threading.Interlocked class's methods. Each of the methods in the Interlocked class performs an atomic read and write operation. In addition, all the Interlocked methods are full memory fences. That is, any variable writes before the call to an Interlocked method execute before the Interlocked method, and any variable reads after the call execute after the call.

The static methods that operate on Int32 variables are by far the most commonly used methods. I show them here.

```
~~~csharp
public static class Interlocked {
    // return (++location)
    public static Int32 Increment(ref Int32 location);

    // return (--location)
    public static Int32 Decrement(ref Int32 location);

    // return (location += value)
    // Note: value can be a negative number allowing subtraction
    public static Int32 Add(ref Int32 location, Int32 value);

    // Int32 old = location; location = value; return old;
    public static Int32 Exchange(ref Int32 location, Int32 value);

    // Int32 old = location;
    // if (location == comparand) location = value;
    // return old;
    public static Int32 CompareExchange(ref Int32 location, Int32 value, Int32 comparand);
    ...
}
~~~
```