
the assignment on the last line is permitted because p1 and p2 are of the same anonymous type.

*end example*

The Equals and GetHashCode methods on anonymous types override the methods inherited from object, and are defined in terms of the Equals and GetHashCode of the properties, so that two instances of the same anonymous type are equal if and only if all their properties are equal.

A member declarator can be abbreviated to a simple name (§11.7.4), a member access (§11.7.6), a null conditional projection initializer (§11.7.7) or a base access (§11.7.13). This is called a projection initializer and is shorthand for a declaration of and assignment to a property with the same name. Specifically, member declarators of the forms

```
«identifier», «expr» . «identifier» and «expr» ? . «identifier»
```

are precisely equivalent to the following, respectively:

```
«identifier» = «identifier», «identifier» = «expr» . «identifier» and «identifier» = «expr» ? . «identifier»
```

Thus, in a projection initializer the identifier selects both the value and the field or property to which the value is assigned. Intuitively, a projection initializer projects not just a value, but also the name of the value.

## 11.7.16 The typeof operator

The typeof operator is used to obtain the System.Type object for a type.

```
typeof_expression
: 'typeof' '(' type ')'
| 'typeof' '(' unbound_type_name ')'
| 'typeof' '(' 'void' ')'
;

unbound_type_name
: identifier generic_dimension_specifier?
| identifier '::' identifier generic_dimension_specifier?
| unbound_type_name '.' identifier generic_dimension_specifier?
;

generic_dimension_specifier
: '<' comma* '>'
;

comma
: ','
;
```

The first form of typeof_expression consists of a typeof keyword followed by a parenthesized type. The result of an expression of this form is the System.Type object for the indicated type. There is only one System.Type object for any given type. This means that for a type T, typeof(T) == typeof(T) is always true. The type cannot be dynamic.

The second form of typeof_expression consists of a typeof keyword followed by a parenthesized unbound_type_name.

Note: An unbound_type_name is very similar to a type_name (§7.8) except that an unbound_type_name contains generic_dimension_specifiers where a type_name contains type_argument_lists. end note

When the operand of a typeof_expression is a sequence of tokens that satisfies the grammars of both unbound_type_name and type_name, namely when it contains neither a generic_dimension_specifier nor a type_argument_list, the sequence of tokens is considered to be a type_name. The meaning of an unbound_type_name is determined as follows:

- Convert the sequence of tokens to a type_name by replacing each generic_dimension_specifier with a type_argument_list having the same number of commas and the keyword object as each type_argument.
- Evaluate the resulting type_name, while ignoring all type parameter constraints.
- The unbound_type_name resolves to the unbound generic type associated with the resulting constructed type (§8.4).

The result of the typeof_expression is the System.Type object for the resulting unbound generic type.

The third form of typeof_expression consists of a typeof keyword followed by a parenthesized void keyword. The result of an expression of this form is the System.Type object that represents the absence of a type. The type object returned by typeof(void) is distinct from the type object returned for any type.

Note: This special type object is useful in class libraries that allow reflection onto methods in the language, where those methods wish to have a way to represent the return type of any method, including void methods, with an instance of System.Type. end note

The typeof operator can be used on a type parameter. The result is the System.Type object for the run-time type that was bound to the type parameter. The typeof operator can also be used on a constructed type or an unbound generic type (§8.4.4). The System.Type object for an unbound generic type is not the same as the System.Type object of the instance type (§14.3.2). The instance type is always a closed constructed type at run-time so its System.Type object depends on the run-time type arguments in use. The unbound generic type, on the other hand, has no type arguments, and yields the same System.Type object regardless of runtime type arguments.

Example: The example

```
using System;
class X<T>
{
    public static void PrintTypes()
    {
        Type[] t =
        {
            typeof(int),
            typeof(System.Int32),
            typeof(string),
            typeof(double[]),
            typeof(void),
            typeof(T),
            typeof(X<T>),
            typeof(X<X<T>>),
            typeof(X<>)
        };
        for (int i = 0; i < t.Length; i++)
        {
            Console.WriteLine(t[i]);
        }
    }
}
class Test
{
    static void Main()
    {
        X<int>.PrintTypes();
    }
}
```

produces the following output:

System.Int32
System.Int32
System.String
System.Double[]
System.Void
System.Int32
X'1[System.Int32]
X'1[X'1[System.Int32]]
X'1[T]

Note that int and System.Int32 are the same type. The result of typeof(X<>) does not depend on the type argument but the result of typeof(X<T>) does.

*end example*

## 11.7.17 The sizeof operator

The sizeof operator returns the number of 8-bit bytes occupied by a variable of a given type. The type specified as an operand to sizeof shall be an unmanaged_type (§8.8).

```
sizeof_expression
    : 'sizeof' '(' unmanaged_type ')'
    ;
```

For certain predefined types the sizeof operator yields a constant int value as shown in the table below:

| Expression | Result |
|---|---|
| sizeof(sbyte) | 1 |
| sizeof(byte) | 1 |
| sizeof(short) | 2 |
| sizeof(ushort) | 2 |
| sizeof(int) | 4 |
| sizeof(uint) | 4 |
| sizeof(long) | 8 |
| sizeof(ulong) | 8 |
| sizeof(char) | 2 |
| sizeof(float) | 4 |
| sizeof(double) | 8 |
| sizeof(bool) | 1 |
| sizeof(decimal) | 16 |

For an enum type T, the result of the expression sizeof(T) is a constant value equal to the size of its underlying type, as given above. For all other operand types, the sizeof operator is specified in §22.6.9.

## 11.7.18 The checked and unchecked operators

The checked and unchecked operators are used to control the overflow-checking context for integral-type arithmetic operations and conversions.

```
checked_expression
  : 'checked' '(' expression ')'
  ;

unchecked_expression
  : 'unchecked' '(' expression ')'
  ;
```

The checked operator evaluates the contained expression in a checked context, and the unchecked operator evaluates the contained expression in an unchecked context. A checked_expression or unchecked_expression corresponds exactly to a parenthesized_expression (§11.7.5), except that the contained expression is evaluated in the given overflow checking context.

The overflow checking context can also be controlled through the checked and unchecked statements (§12.12).

The following operations are affected by the overflow checking context established by the checked and unchecked operators and statements:

- The predefined ++ and -- operators (§11.7.14 and §11.8.6), when the operand is of an integral or enum type.
- The predefined - unary operator (§11.8.3), when the operand is of an integral type.
- The predefined +, -, *, and / binary operators (§11.9), when both operands are of integral or enum types.
- Explicit numeric conversions (§10.3.2) from one integral or enum type to another integral or enum type, or from float or double to an integral or enum type.

When one of the above operations produces a result that is too large to represent in the destination type, the context in which the operation is performed controls the resulting behavior:

- In a checked context, if the operation is a constant expression (§11.20), a compile-time error occurs. Otherwise, when the operation is performed at run-time, a System.OverflowException is thrown.
- In an unchecked context, the result is truncated by discarding any high-order bits that do not fit in the destination type.

For non-constant expressions (§11.20) (expressions that are evaluated at run-time) that are not enclosed by any checked or unchecked operators or statements, the default overflow checking context is unchecked, unless external factors (such as compiler switches and execution environment configuration) call for checked evaluation.
