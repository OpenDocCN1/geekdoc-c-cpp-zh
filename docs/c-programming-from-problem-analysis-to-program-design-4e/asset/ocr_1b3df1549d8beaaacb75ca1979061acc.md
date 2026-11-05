It is possible to use exactly the same name as an identifier for a local variable that has already been used for an instance variable or a parameter identifier. When this happens, the innermost declaration takes scope when you are inside that method. Thus, the local variable would be visible and the other(s) hidden. If, for example, the identifier `feet` is used as a variable in the `Main()` method and that same identifier, `feet`, is declared as a variable inside the `GetLength()` method, no syntax error is generated. Instead, the `feet` variable declared in the `GetLength()` method is visible as long as execution is inside that method. When the method is completed, the `GetLength()` `feet` identifier becomes out of scope. You can think of it as “dying” or no longer existing as soon as the closing curly brace is encountered. As soon as that happens, if control returns back to `Main()` where the other `feet` is declared, the `Main()` method’s `feet` goes back into scope and becomes visible again.

> **NOTE** — Be cautious about declaring local variables using a name that is already associated with another variable. This often leads to unreadable code that is more difficult to debug and maintain.

Like nonvalue-returning methods, one or more data items can be passed as arguments to these types of methods, as illustrated in Example 3–16.

# EXAMPLE 3.16

```
public static double DeterminePrice(double squareYards,
                                    double pricePerSquareYard)
{
    return (pricePerSquareYard * squareYards);
}
```

Calls to value-returning methods require a location for the value to be returned. As you saw previously, calls can be placed in assignment statements, output statements, or anywhere a value can be used. If the method has parameters, the call includes the actual data inside the parentheses. Because the `static` keyword appears in the heading, these are still considered `class` methods. Calls to methods in Examples 3–15 and 3–16 follow:

```
double roomLength;
roomLength = GetLength();
Console.WriteLine("Total cost of the carpet: {0:C}",
                  DeterminePrice(squareYards, pricePerSquareYard));
```

An error would be generated if you place a call to a nonvalue-returning method as an argument to the `Write()` or `WriteLine()` methods. Both of these methods are expecting to receive a value back from a method so that the value can be displayed. Placing a call to the `DeterminePrice()` method is an appropriate argument to the `WriteLine()` method because `DeterminePrice()` returns a `double`.