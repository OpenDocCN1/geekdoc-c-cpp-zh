+   1. Operators in expressions contained within pairs of parentheses are evaluated first. Parentheses are said to be at the “highest level of precedence.” In cases of **nested**, or **embedded**, parentheses, such as:
+   
+      `( a + ( b + c ) )`
+   
+      the operators in the *innermost* pair of parentheses are applied first.

+   2. Multiplication, division and modulus operations are applied next. If an expression contains several multiplication, division and modulus operations, operators are applied from *left to right*. Multiplication, division and modulus are said to be on the *same level* of precedence.

+   3. Addition and subtraction operations are applied last. If an expression contains several addition and subtraction operations, operators are applied from *left to right*. Addition and subtraction also have the *same level* of precedence.

The set of rules of operator precedence defines the order in which C++ applies operators. When we say that certain operators are applied from left to right, we are referring to the **associativity** of the operators. For example, the addition operators (+) in the expression

```
a + b + c
```

associate from left to right, so a + b is calculated first, then c is added to that sum to determine the whole expression’s value. We’ll see that some operators associate from right to left. Figure 2.10 summarizes these rules of operator precedence. We can add this table as we introduce additional C++ operators. A complete precedence chart is included in Appendix A.

| Operator(s) | Operation(s) | Order of evaluation (precedence) |
|---|---|---|
| `( )` | Parentheses | Evaluated first. If the parentheses are nested, the expression in the innermost pair is evaluated first. **[Caution:** If you have an expression such as `(a + b) * (c − d)` in which two sets of parentheses are not nested, but appear “on the same level,” the C++ Standard does not specify the order in which these parenthesized subexpressions will be evaluated.**] |
| `*, /, %` | Multiplication, Division, Modulus | Evaluated second. If there are several, they’re evaluated left to right. |
| `+`<br>`−` | Addition<br>Subtraction | Evaluated last. If there are several, they’re evaluated left to right. |

**Fig. 2.10** | Precedence of arithmetic operators.

# Sample Algebraic and C++ Expressions

Now consider several expressions in light of the rules of operator precedence. Each example lists an algebraic expression and its C++ equivalent. The following is an example of an arithmetic mean (average) of five terms:

```
Algebra:     m = (a + b + c + d + e) / 5
C++:         m = ( a + b + c + d + e ) / 5;
```