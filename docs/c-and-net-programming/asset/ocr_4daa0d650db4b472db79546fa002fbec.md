+   - For the two bitwise shift operators, `<<` and `>>`, the first argument must be the class in which one is working and the second argument must by a constant integer (type `int`).

# 13. Comparison Operators

As the name implies, a comparison is used to find out whether one of the two values is higher than the other. The values must be of the same type. Comparison operators work in pair.

That is, if one wants to compare two values for equality, one must also be able to know when they are different. For this reason, a **comparison operator is to be overloaded**, then its **opposite also needs to be overloaded**. That is,

+   - If `==` is overloaded, `!=` must also be overloaded.
+   - If `<` overloaded, `>` must also be overloaded and vice versa.
+   - If `<=` is overloaded, `>=` must be overloaded and vice versa.

# Example

```
using System;

class NumberOps
{
    public int val;

    public static NumberOps operator + (NumberOps obj1, NumberOps obj2)
    {
        // Add two numbers and return a new number
        NumberOps numop = new NumberOps ();
        numop.val = obj1.val + obj2.val;
        return numop;
    }

    public static NumberOps operator ++ (NumberOps obj)
    {
        // Increment this object
        obj.val++;
        return obj;
    }
}

class OpOverload
{
    static void Main()
    {
        // Increment widget twice.
        NumberOps ob = new NumberOps ();
```