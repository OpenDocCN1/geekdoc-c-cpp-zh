Defining the conversion operators in the preceding Rational type allows you to write code like (in C#).

```
public sealed class Program {
    public static void Main()
    {
        Rational r1 = 5; // Implicit cast from Int32 to Rational
        Rational r2 = 2.5F; // Implicit cast from Single to Rational

        Int32 x = (Int32) r1; // Explicit cast from Rational to Int32
        Single s = (Single) r2; // Explicit cast from Rational to Single
    }
}
```

Under the covers, the C# compiler detects the casts (type conversions) in the code and internally generates IL code that calls the conversion operator methods defined by the Rational type. But what are the names of these methods? Well, compiling the Rational type and examining its data shows that the compiler produces one method for each conversion operator defined. For the Rational type, the metadata for the four conversion operator methods looks like this:

```
public static Rational op_Implicit(Int32 num)
public static Rational op_Implicit(Single num)
public static Int32 op_Explicit(Rational r)
public static Single op_Explicit(Rational r)
```

As you can see, methods that convert an object from one type to another are always named op_Implicit or op_Explicit. You should define an implicit conversion operator when precision or magnitude is not lost during a conversion, such as converting an Int32 to a Rational. You should define an explicit conversion operator if precision or magnitude is lost during the conversion, when converting a Rational object to an Int32. If an explicit conversion fails, you should indicate this by having your conversion operator method throw an OverflowException or InvalidOperationException.

> The two op_Explicit methods take the same parameter, a Rational. However, the methods differ by their return type, an Int32 and a Single. This is an example of methods that differ only by their return type. The CL fully supports the ability to define multiple methods that differ only by return type. However, very few languages expose this ability. You're probably aware, C+, Visual Basic, and Java are all examples of languages that don't support the definition of multiple methods that differ only by their return type. A few languages (such as IL assembly language) allow the developer to explicitly select which of these methods to call. Of course, IL assembly language programmers shouldn't take advantage of this ability because they define it be callable from other programming languages. Even though C# doesn't expose this ability to the C# programmer, the compiler does take advantage of this ability internally when a type defines conversion operator methods.

![](bbox=[0.105, 0.615, 0.135, 0.645])