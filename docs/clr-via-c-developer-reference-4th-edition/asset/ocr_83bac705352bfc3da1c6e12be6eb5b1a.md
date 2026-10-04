that the operator is defined within. The reason for this restriction is that it enables the C# compiler to search for a possible method to bind to in a reasonable amount of time.

Here is an example of an operator overload method defined in a C# class definition.

```
public sealed class Complex {
    public static Complex operator+(Complex c1, Complex c2) { ... }
}
```

The compiler enters a metadata definition for an entry called _Add; the method entry also has the special flag set, indicating that this is a "special" method. When language compilers (including the C# compiler) see a + operator specified in source code, they look to see if one of the operand's types defines a specialname called _Add which addition parameters are compatible with the operand's types. If this method exists, the compiler emits code to this method. If no method exists, a compilation error occurs.

Tables 8-1 and 8-2 show the set of unary and binary operators that C# supports being overloaded, their symbols, and the corresponding Common Language Specification (CLS) method name that the compiler emits. I explain the three columns in the next section.

# TABLE 8-1 C Unary Operators and Their CLS-Compliant Method Names

| C Operator Symbol | Special Method Name | Suggested CLS-Compliant Method Name |
|---|---|---|
| + | op_UnaryPlus | Plus |
| - | op_UnaryNegation | Negate |
| ! | op_LogicalNot | Not |
| ~ | op_OnesComplement | OnesComplement |
| ++ | op_Increment | Increment |
| -- | op_Decrement | Decrement |
| (none) | op_True | IsTrue { get; } |
| (none) | op_False | IsFalse { get; } |

# TABLE 8-2 C Binary Operators and Their CLS-Compliant Method Names

| C Operator Symbol | Special Method Name | Suggested CLS-Compliant Method Name |
|---|---|---|
| + | op_Addition | Add |
| - | op_Subtraction | Subtract |
| * | op_Multiply | Multiply |
| / | op_Division | Divide |
| % | op_Modulus | Mod |
| & | op_BitwiseAnd | BitwiseAnd |
| | | op_BitwiseOr | BitwiseOr |
| ^ | op_ExclusiveOr | Xor |