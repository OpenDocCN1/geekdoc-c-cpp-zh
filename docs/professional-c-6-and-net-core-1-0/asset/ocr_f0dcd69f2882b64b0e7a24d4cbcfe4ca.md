implemented under the hood as a primitive type, so using `decimal` has a performance effect on your calculations.

To specify that your number is a `decimal` type rather than a `double`, a `float`, or an integer, you can append the `M` (or `m`) character to the value, as shown here:

```
decimal d = 12.30M;
```

# The Boolean Type

The C# `bool` type is used to contain Boolean values of either `true` or `false`.

| Name | .NET Type | Description | Significant Figures | Range |
|------|-----------|-------------|---------------------|-------|
| `bool` | `System.Boolean` | Represents true or false | NA | true or false |

You cannot implicitly convert `bool` values to and from integer values. If a variable (or a function return type) is declared as a `bool`, you can only use values of `true` and `false`. You get an error if you try to use zero for `false` and a nonzero value for `true`.

# The Character Type

For storing the value of a single character, C# supports the `char` data type.

| Name | .NET Type | Values |
|------|-----------|--------|
| `char` | `System.Char` | Represents a single 16-bit (Unicode) character |

Literals of type `char` are signified by being enclosed in single quotation marks—for example, `'A'`. If you try to enclose a character in double quotation marks, the compiler treats the character as a string and throws an error.

As well as representing `chars` as character literals, you can represent them with four-digit hex Unicode values (for example, `'\u0041'`), as integer values with a cast (for example, `(char)65`), or as hexadecimal values (for example, `'\x0041'`). You can also represent them with an escape sequence, as shown in the following table.