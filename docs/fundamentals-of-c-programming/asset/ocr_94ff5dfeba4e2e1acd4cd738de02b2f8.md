| Arity | Operators | Associativity |
|---|---|---|
| Unary | +, - | |
| Binary | *, /, % | Left |
| Binary | +, - | Left |
| Binary | = | Right |

Table 4.2: Operator precedence and associativity. The operators in each row have a higher precedence than the operators below it. Operators within a row have the same precedence.

+   • The expression x = (y = z) is evaluated. The value of y = z, that is z, is assigned to x. The overall value of the expression x = y = z is thus the value of z. Now the values of x, y, and z are all equal (to z).

+   • The expression w = (x = y = z) is evaluated. The value of the expression x = y = z is equal to z’s value, so z’s value is assigned to w. The overall value of the expression w = x = y = z is equal to z, and the variables w, x, y, and z are all equal (to z).

As in the case of precedence, we can use parentheses to override the natural associativity within an expression.

The unary operators have a higher precedence than the binary operators, and the unary operators are right associative. This means the statements

```
std::cout << -3 + 2 << '\n';
std::cout << -(3 + 2) << '\n';
```

which display

![](bbox=[0.12, 0.512, 0.8, 0.552])

behave as expected.

Table 4.2 shows the precedence and associativity rules for some C++ operators. The * operator also has a unary form that has nothing to do with mathematics; it is covered in Section 10.7.

# 4.4 Comments

Good programmers annotate their code by inserting remarks that explain the purpose of a section of code or why they chose to write a section of code the way they did. These notes are meant for human readers, not the compiler. It is common in industry for programs to be reviewed for correctness by other programmers or technical managers. Well-chosen identifiers (see Section 3.3) and comments can aid this assessment process. Also, in practice, teams of programmers develop software. A different programmer may be required to finish or fix a part of the program written by someone else. Well-written comments can help others understand new code quicker and increase their productivity modifying old or unfinished code. While it may seem difficult to believe, even the same programmer working on her own code months later can have a difficult time remembering what various parts do. Comments can help greatly.

Any text contained within comments is ignored by the compiler. C++ supports two types of comments: single line comments and block comments:

+   • Single line comment—the first type of comment is useful for writing a single line remark: