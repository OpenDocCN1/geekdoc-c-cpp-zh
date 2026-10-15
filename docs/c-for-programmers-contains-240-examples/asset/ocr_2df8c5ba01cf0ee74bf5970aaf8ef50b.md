+   1. Operators in expressions contained within pairs of parentheses are evaluated first. Parentheses are said to be at the “highest level of precedence.” In cases of *nested*, or *embedded, parentheses*, such as
+   
+       ( ( a + b ) + c )
+   
+   the operators in the innermost pair of parentheses are applied first. [*Note: As in algebra, it is acceptable to place unnecessary parentheses in an expression to make the expression clearer. These are called *redundant parentheses.*]
+   2. Multiplication, division and modulus operations are applied next. If an expression contains several multiplication, division and modulus operations, operators are applied from left to right. Multiplication, division and modulus are said to be on the same level of precedence.
+   3. Addition and subtraction operations are applied last. If an expression contains several addition and subtraction operations, operators are applied from left to right. Addition and subtraction also have the same level of precedence.

The set of rules of operator precedence defines the order in which C++ applies operators. When we say that certain operators are applied from left to right, we are referring to the *associativity* of the operators. For example, in the expression

    a + b + c

the addition operators (+) associate from left to right, so a + b is calculated first, then c is added to that sum to determine the value of the whole expression. We’ll see that some operators associate from right to left. Figure 2.7 summarizes these rules of operator precedence. This table will be expanded as additional C++ operators are introduced. A complete precedence chart is included in Appendix A.

# Good Programming Practice 2.5

Using redundant parentheses in complex arithmetic expressions can make the expressions clearer.

| Operator(s) | Operation(s) | Order of evaluation (precedence) |
|---|---|---|
| ( ) | Parentheses | Evaluated first. If the parentheses are nested, the expression in the innermost pair is evaluated first. If there are several pairs of parentheses “on the same level” (i.e., not nested), they are evaluated left to right. |
| * | Multiplication, | Evaluated second. If there are several, they are evaluated left to right. |
| / | Division, | |
| % | Modulus | |
| + | Addition | Evaluated last. If there are several, they are evaluated left to right. |
| - | Subtraction | |

Fig. 2.7 | Precedence of arithmetic operators.