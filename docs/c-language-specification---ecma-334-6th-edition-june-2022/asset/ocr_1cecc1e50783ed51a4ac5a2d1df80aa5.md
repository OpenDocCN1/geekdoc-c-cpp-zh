+   - All types referenced in an operator declaration shall be at least as accessible as the operator itself (§7.5.5).
+   - It is an error for the same modifier to appear multiple times in an operator declaration.

Each operator category imposes additional restrictions, as described in the following subclauses.

Like other members, operators declared in a base class are inherited by derived classes. Because operator declarations always require the class or struct in which the operator is declared to participate in the signature of the operator, it is not possible for an operator declared in a derived class to hide an operator declared in a base class. Thus, the new modifier is never required, and therefore never permitted, in an operator declaration.

Additional information on unary and binary operators can be found in §11.4.

Additional information on conversion operators can be found in §10.5.

# 14.10.2 Unary operators

The following rules apply to unary operator declarations, where T denotes the instance type of the class or struct that contains the operator declaration:

+   - A unary +, -, |, or ~ operator shall take a single parameter of type T or T? and can return any type.
+   - A unary ++ or -- operator shall take a single parameter of type T or T? and shall return that same type or a type derived from it.
+   - A unary true or false operator shall take a single parameter of type T or T? and shall return type bool.

The signature of a unary operator consists of the operator token (+, -, !, ~, ++, --, true, or false) and the type of the single formal parameter. The return type is not part of a unary operator's signature, nor is the name of the formal parameter.

The true and false unary operators require pair-wise declaration. A compile-time error occurs if a class declares one of these operators without also declaring the other. The true and false operators are described further in §11.21.

Example: The following example shows an implementation and subsequent usage of operator++ for an integer vector class

```
public class IntVector
{
    public IntVector(int length) {...}
    public int Length { ... }    // Read-only property
    public int this[int index] { ... }  // Read-write indexer

    public static IntVector operator++(IntVector iv)
    {
        IntVector temp = new IntVector(iv.Length);
        for (int i = 0; i < iv.Length; i++)
        {
            temp[i] = iv[i] + 1;
        }
        return temp;
    }
}
```