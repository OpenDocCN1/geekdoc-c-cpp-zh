The following code samples illustrate how you can use the logical operators along with the relational operators in expressions:

+   - `(number1 > number2) || (number1 == 10)` evaluates to `true` because the first expression evaluates to `false`, 10 is not greater than 15, and the second expression evaluates to `true`, 10 is equal to 10. Only one expression needs to be true using OR logic for the entire expression to be `true`.
+   - `(number1 > number2) && (number1 == 10)` evaluates to `false` because the first expression is `false`, 10 is not greater than 15, and the second expression is `true`, 10 is equal to 10. Using AND logic, both expressions must be `true` for the entire expression to be `true`.
+   - `(number1 != number2) && (number1 == 10)` evaluates to `true` because both expressions are `true`; that is, 10 is not equal to 15 and 10 is equal to 10. Using AND logic, if both expressions are `true`, then the entire expression is `true`.
+   - `!(number1 == number2)` evaluates to `true` because the expression evaluates to `false`, 10 is not equal to 15. The `!` operator then reverses `false`, which results in a `true` value.

# RELATIONAL AND LOGICAL OPERATOR PRECEDENCE AND ASSOCIATIVITY

Like the arithmetic operators discussed in Chapter 2, the relational and logical operators are evaluated according to specific rules of associativity and precedence. Table 4-3 shows the precedence and associativity of the operators discussed thus far in this book.

| Operator Name | Operator Symbol(s) | Order of Precedence | Associativity |
|---|---|---|---|
| Parentheses | `()` | First | Left to right |
| Unary | `- + !` | Second | Right to left |
| Multiplication, division, and modulus | `* / %` | Third | Left to right |
| Addition and subtraction | `+ -` | Fourth | Left to right |
| Relational | `< > <= >=` | Fifth | Left to right |
| Equality | `== !=` | Sixth | Left to right |
| AND | `&&` | Seventh | Left to right |
| OR | `&#124;&#124;` | Eighth | Left to right |
| Assignment | `= += -= *= /= %=` | Ninth | Right to left |

Table 4-3 Order of precedence and associativity

> > **NOTE** Some symbols appear in Table 4-3 more than once because they have more than one meaning. For example, when the − operator is used before a number or a variable that contains a number, it is interpreted as the unary − operator. When the − operator is used between operands, it is interpreted as the subtraction operator.