# Operator Overloading

The preceding chapter looked at implementing value equality behavior and provided the guideline that the class should also implement == and !=. Implementing any operator is called operator overloading. This section describes how to perform such overloading not only for == and !=, but also for other supported operators.

For example, string provides a + operator that concatenates two strings. This is perhaps not noteworthy, because string is a predefined type, so it could possibly have special compiler support. C# provides for adding + operator to a class or struct. In fact, all operators are supported except x.,y, f(x), new, typeof, default, unchecked, delegate, is, as, =, and =>. One noteworthy operator that cannot be implemented is the assignment operator; there is no way to change the behavior of = = operator.

Before going the exercise of implementing an operator overload, consider that such operators are not discoverable by IntelliSense. Unless the intent is for a type to act like a primitive type (e.g., a numeric type), you should avoid overloading operator as the only means of accessing the behavior.

# Comparison Operators (==, !=, <, <=, >=)

In Chapter 9 (https://essentialcsharp.com/implementing-value-equality) we reviewed the code generated for a record's implementation of the == and != operators. In addition, you can override the greater and less than operators, when combined with equality checks (see Listing 10.1).

+   LISTING 10.1: Implementing the == and != Operators

```
public sealed class ProductSerialNumber
{
    // ...

    public static bool operator ===(
        ProductSerialNumber leftHandSide,
        ProductSerialNumber rightHandSide)
    {
        // Check if leftHandSide is null
        // (operator == would be recursive)
        if(leftHandSide == null)
```