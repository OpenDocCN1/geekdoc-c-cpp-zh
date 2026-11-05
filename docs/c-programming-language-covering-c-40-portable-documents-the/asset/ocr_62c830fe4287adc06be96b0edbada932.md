> **VLADIMIR RESHETNIKOV** Be aware that the default implementation of the Equals method in value types can use bitwise comparison in some cases to speed up performance. If two instances of your value type contain in their fields positive and negative zero, respectively, they can compare as not equal. You can override the Equals method to change the default behavior.

```
```csharp
using System;
struct S
{
    double X;
    static void Main()
    {
        var a = new S { X = 0.0 };
        var b = new S { X = -0.0 };
        Console.WriteLine(a.X.Equals(b.X)); // True
        Console.WriteLine(a.Equals(b)); // False
    }
}
```
```

> **PETER SESTOFT** Some of the confusion over negative zero may stem from the fact that the current implementations of C# print positive and negative zero in the same way, as 0.0, and no combination of formatting parameters seems to affect that display. Although this is probably done with the best of intentions, it is unfortunate. To reveal a negative zero, you must resort to strange-looking code like this, which works because 1/(-0.0) = -Infinity < 0:

```
```csharp
public static string DoubleToString(double d) {
    if (d == 0.0 && 1/d < 0)
        return "-0.0";
    else
        return d.ToString();
}
```
```

+   - Positive infinity and negative infinity. Infinities are produced by such operations as dividing a non-zero number by zero. For example, 1.0 / 0.0 yields positive infinity, and -1.0 / 0.0 yields negative infinity.
+   - The Not-a-Number value, often abbreviated NaN. NaNs are produced by invalid floating point operations, such as dividing zero by zero.

> **PETER SESTOFT** A large number of distinct NaNs exist, each of which has a different "payload." See the annotations on §7.8.1.