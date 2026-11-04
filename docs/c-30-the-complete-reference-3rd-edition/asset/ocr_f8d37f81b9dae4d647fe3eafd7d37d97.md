better solution in many cases), it is still important that you understand how they work
because of their integral importance to LINQ.

An extension method is a static method that must be contained within a static, non-generic
class. The type of its first parameter determines the type of objects on which the extension
method can be called. Furthermore, the first parameter must be modified by this. The object on
which the method is invoked is passed automatically to the first parameter. It is not explicitly
passed in the argument list. A key point is that even though an extension method is declared
static, it can still be called on an object, just as if it were an instance method.

Here is the general form of an extension method:

```
```
static ret-type name(this invoked-on-type ob, param-list)
```
```

Of course, if there are no arguments other than the one passed implicitly to ob, then param-list
will be empty. Remember, the first parameter is automatically passed the object on which
the method is invoked. In general, an extension method will be a public member of its class.

Here is an example that creates three simple extension methods:

```
```csharp
// Create and use some extension methods.
using System;

static class MyExtMeths {

    // Return the reciprocal of a double.
    public static double Reciprocal(this double v) {
        return 1.0 / v;
    }

    // Reverse the case of letters within a string and
    // return the result.
    public static string RevCase(this string str) {
        string temp = "";

        foreach(char ch in str) {
            if(Char.IsLower(ch)) temp += Char.ToUpper(ch);
            else temp += Char.ToLower(ch);
        }
        return temp;
    }

    // Return the absolute value of n / d.
    public static double AbsDivideBy(this double n, double d) {
        return Math.Abs(n / d);
    }
}

class ExtDemo {
    static void Main() {
        double val = 8.0;
        string str = "Alpha Beta Gamma";

        // Call the Recip() extension method.
        Console.WriteLine("Reciprocal of {0} is {1}",
                          val, val.Reciprocal());
    }
}
```
```