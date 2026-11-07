To refer to a particular location or element in the array, we specify the array’s name, followed by the element’s position number in square brackets ([]). The first element is located at position number 0 (zero). The position number is called the element’s subscript (or index). A subscript must be a non-negative integer or integer expression.

Let’s examine the array in the previous diagram more closely. The array’s name is `c`. The value of `c[0]` is −45, `c[2]` is 0 and `c[4]` is 1543. A subscripted array name is an lvalue that can be used on the left side of an assignment. So, the statement:

```
c[2] = 1000;
```

replaces `c[2]`’s current value (0) with the value 1000. To print the sum of the values in array `c`’s first three elements, we’d write:

```
printf("%d", c[0] + c[1] + c[2]);
```

To divide the value of element 3 of array `c` by 2 and assign the result to the variable `x`, write:

```
x = c[3] / 2;
```

The brackets that enclose an array’s subscript are an operator with the highest level of precedence. The following table shows the precedence and grouping of the operators introduced to this point in the text:

| Operators | Grouping | Type |
|---|---|---|
| `[]` `()` `++ (postfix)` `-- (postfix)` | left to right | highest |
| `+` `-` `!` `++ (prefix)` `-- (prefix)` `(type)` | right to left | unary |
| `*` `/` `%` | left to right | multiplicative |
| `+` `-` | left to right | additive |
| `<` `<=` `>` `>=` | left to right | relational |
| `==` `!=` | left to right | equality |
| `&&` | left to right | logical AND |
| `\|\|` | left to right | logical OR |
| `?:` | right to left | conditional |
| `=` `+=` `-=` `*=` `/=` `%=` | right to left | assignment |
| `,` | left to right | comma |

# Self Check

+   1. *(Multiple Choice)* Which of the following statements is *false*?
+      a) Any array element may be referred to by giving the array’s name followed by the element’s position number in square brackets (`[]`).
+      b) Every array’s first element has position number 1.
+      c) An array name, like other identifiers, can contain only letters, digits and underscores and cannot begin with a digit.