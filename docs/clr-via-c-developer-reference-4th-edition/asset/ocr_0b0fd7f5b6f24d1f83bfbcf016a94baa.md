Here is a somewhat contrived example of a type that defines a type parameter and a method that has its own unique type parameter.

```
internal sealed class GenericType<T> {
    private T m_value;

    public GenericType(T value) { m_value = value; }

    public TOutput Converter<TOutput>() {
        TOutput result = (TOutput) Convert.ChangeType(m_value, typeof(TOutput));
        return result;
    }
}
```

In this example, you can see that the Generic class defines its own type parameter (T), and the Converter method defines its own type parameter (TOutput). This allows a GenericType to be constructed with any type. The Converter can convert the object referred by the m_value field to various types depending on what argument is passed to it when called. The ability to have type parameters and method parameters allows for flexibility.

A reasonably good example of a generic method is the Swap method.

```
private static void Swap<T>(ref T o1, ref T o2) {
    T temp = o1;
    o1 = o2;
    o2 = temp;
}
```

Code can now call Swap as follows.

```
private static void CallingSwap() {
    Int n1 = 1, n2 = 2;
    Console.WriteLine("n1={0}, n2={1}", n1, n2);
    Swap(ref n1, ref n2);
    Console.WriteLine("n1={0}, n2={1}", n1, n2);

    String s1 = "Aidan", s2 = "Grant";
    Console.WriteLine("s1={0}, s2={1}", s1, s2);
    Swap(ref s1, ref s2);
    Console.WriteLine("s1={0}, s2={1}", s1, s2);
}
```

Using generic methods that take out and ref parameters can be particularly interesting because the variable you pass as an out/ref argument must be the same type as the parameter to avoid a potential type safety exploit. This issue related to out/ref parameters is discussed towards the end of the "Parameters by Reference to a Method" section in Chapter 9, "Parameters." In fact, the Interlocked class's Exchange and CompareExchange methods offer generic overloads for precisely this reason.¹

> ¹ The where will be explained in the "Verifiability and Constraints" section later in this chapter.