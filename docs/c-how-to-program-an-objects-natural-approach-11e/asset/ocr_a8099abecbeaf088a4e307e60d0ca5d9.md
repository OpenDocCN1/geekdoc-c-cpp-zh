# Parentheses for Grouping Subexpressions

Parentheses are used in C++ expressions in the same manner as in algebraic expressions.
For example, to multiply x times the quantity y + z, we write x × (y + z).

# Rules of Operator Precedence

C++ applies the operators in arithmetic expressions in a precise order determined by the following rules of operator precedence, which are generally the same as those in algebra:

+   1. Expressions in parentheses evaluate first. Parentheses are said to be at the “highest level of precedence.” In cases of nested or embedded parentheses, as in the following statement, expressions in the innermost pair of parentheses evaluate first:
+   
+      `(a * (b + c))`
+   
+   2. Multiplication, division and remainder operations evaluate next. In an expression containing several of these operations, they’re applied from left to right. These three operators have the same level of precedence.
+   
+   3. Addition and subtraction operations evaluate last and are applied from left to right. Addition and subtraction have the same level of precedence.

You can view the complete operator precedence chart at https://en.cppreference.com/w/cpp/language/operator_precedence. **Caution:** In an expression with two sets of parentheses “on the same level,” such as `(a + b) * (c − d)`, the C++ Standard does not specify the order in which these parenthesized subexpressions will evaluate.

# Operator Grouping

When we say that C++ applies certain operators from left to right, we are referring to the operators’ grouping (sometimes called associativity). For example, in the expression

`a + b + c`

the addition operators (+) group from left-to-right as if we parenthesized the expression as `(a + b) + c`. Most C++ operators of the same precedence group from left to right. We’ll see that some operators group from right to left.

# Sample Algebraic and C++ Expressions

Now consider several expressions in light of the rules of operator precedence. Each example lists an algebraic expression and its C++ equivalent. The following is an example of an arithmetic mean (average) of five terms:

Algebra:  m = (a + b + c + d + e) / 5

C++:       m = (a + b + c + d + e) / 5;

The parentheses are required because division has higher precedence than addition. The entire quantity (a + b + c + d + e) is to be divided by 5. If the parentheses are erroneously omitted, we obtain a + b + c + d + e / 5, which evaluates incorrectly as

a + b + c + d + e / 5

The following is an example of the equation of a straight line:

Algebra:  y = mx + b

C++:       y = m * x + b;