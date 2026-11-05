In Example 5–2, up to position 19, the strings are considered equal. When the characters at position 19 are compared, the result of the expression `(false)` is determined, and no additional comparison beyond position 19 is needed.

![](bbox=[0.173, 0.16, 0.237, 0.211])

Many languages require you to use special `string` methods, such as `strcmp( )`, to make equality comparisons on `string` variables. C# makes it much easier for you to write instructions comparing the contents of `string` variables for equality.

# Relational Operators

**Relational operators** allow you to test variables to see if one is greater or less than another variable or value. Table 5–2 lists the relational symbols used in C#. The symbol’s meaning and a sample expression using each operator is included.

**Table 5-2 Relational symbols**

| Symbol | Meaning | Example | Result |
|---|---|---|---|
| `>` | Greater than | `(8 > 5)`<br>`(1 > 2)` | `true`<br>`false` |
| `<` | Less than | `(1 < 2)`<br>`('z' < 'a')` | `true`<br>`false` |
| `>=` | Greater than or equal | `(100 >= 100)`<br>`(14 >= 7)` | `true`<br>`true` |
| `<=` | Less than or equal | `(100 <= 100)`<br>`(27 <= 7)` | `true`<br>`false` |

For comparing numbers, the relational operators <, >, <=, and >= produce a straightforward result, as shown in Table 5–2. When you compare characters declared using `char`, they are compared lexicographically using the Unicode character set. A comparison to determine whether the lowercase character z is less than a produces `false`, because z has a Unicode decimal equivalent of 122 and a has a value of 97.

![](bbox=[0.173, 0.679, 0.237, 0.729])

You cannot compare `string` operands using the relational symbols <, >, >=, or <= in C#.

Remember from Chapter 2 that strings in C# are reference types. Instead of the `string` character values being stored in binary form at the memory location of the variable’s identifier, the memory location of a `string` identifier contains the address in which the string of characters is stored. Normally when you compare reference type variables, you get a comparison of the addresses.

![](bbox=[0.174, 0.855, 0.237, 0.906])

The `string` class in C# has a number of useful methods for dealing with strings. You learn about these methods in Chapter 7. The `Compare( )` method is used for relational comparisons of strings. If you want to look ahead, many methods of the `string` class are listed in Table 7–3.