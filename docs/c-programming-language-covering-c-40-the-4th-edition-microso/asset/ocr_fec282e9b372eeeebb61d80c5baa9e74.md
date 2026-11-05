The true and false unary operators require pairwise declaration. A compile-time error occurs if a class declares one of these operators without also declaring the other. The true and false operators are described further in §7.12.2 and §7.20.

The following example shows an implementation and subsequent usage of operator ++ for an integer vector class:

```
```csharp
public class IntVector
{
    public IntVector(int length) {...}
    public int Length {...}                  // Read-only property
    public int this[int index] {...}         // Read-write indexer
    public static IntVector operator ++(IntVector iv) {
        IntVector temp = new IntVector(iv.Length);
        for (int i = 0; i < iv.Length; i++)
            temp[i] = iv[i] + 1;
        return temp;
    }
}
class Test
{
    static void Main() {
        IntVector iv1 = new IntVector(4);    // Vector of 4 x 0
        IntVector iv2;

        iv2 = iv1++;                          // iv2 contains 4 x 0, iv1 contains 4 x 1
        iv2 = ++iv1;                          // iv2 contains 4 x 2, iv1 contains 4 x 2
    }
}
```
```

Note how the operator method returns the value produced by adding 1 to the operand, just like the postfix increment and decrement operators (§7.6.9) and the prefix increment and decrement operators (§7.7.5). Unlike in C++, this method need not modify the value of its operand directly. In fact, modifying the operand value would violate the standard semantics of the postfix increment operator.

# 10.10.2 Binary Operators

The following rules apply to binary operator declarations, where T denotes the instance type of the class or struct that contains the operator declaration:

+   - A binary nonshift operator must take two parameters, at least one of which must have type T or T?, and can return any type.
+   - A binary << or >> operator must take two parameters, the first of which must have type T or T? and the second of which must have type int or int?, and can return any type.