```
static int F() => checked(Multiply(1000000, 1000000));
}
```

the use of checked in F does not affect the evaluation of x * y in Multiply, so x * y is evaluated in the default overflow checking context.

end example

The unchecked operator is convenient when writing constants of the signed integral types in hexadecimal notation.

Example:

```
class Test
{
    public const int AllBits = unchecked((int)0xFFFFFFFF);
    public const int HighBit = unchecked((int)0x80000000);
}
```

Both of the hexadecimal constants above are of type uint. Because the constants are outside the int range, without the unchecked operator, the casts to int would produce compile-time errors.

end example

Note: The checked and unchecked operators and statements allow programmers to control certain aspects of some numeric calculations. However, the behavior of some numeric operators depends on their operands' data types. For example, multiplying two decimals always results in an exception on overflow even within an explicitly unchecked construct. Similarly, multiplying two floats never results in an exception on overflow even within an explicitly checked construct. In addition, other operators are never affected by the mode of checking, whether default or explicit. end note

# 11.7.19 Default value expressions

A default value expression is used to obtain the default value (§9.3) of a type. Typically a default value expression is used for type parameters, since it might not be known if the type parameter is a value type or a reference type. (No conversion exists from the null literal (§6.4.5.7) to a type parameter unless the type parameter is known to be a reference type (§8.2).)

```
default_value_expression
    : 'default' '(' type ')'
    ;
```

If the type in a default_value_expression evaluates at run-time to a reference type, the result is null converted to that type. If the type in a default_value_expression evaluates at run-time to a value type, the result is the value type's default value (§8.3.3).

A default_value_expression is a constant expression (§11.20) if type is a reference type or a type parameter that is known to be a reference type (§8.2). In addition, a default_value_expression is a constant expression if the type is one of the following value types: sbyte, byte, short, ushort, int, uint, long, ulong, char, float, double, decimal, bool, or any enumeration type.

# 11.7.20 Nameof expressions

A nameof_expression is used to obtain the name of a program entity as a constant string.

```
nameof_expression
    : 'nameof' '(' named_entity ')'
    ;
```