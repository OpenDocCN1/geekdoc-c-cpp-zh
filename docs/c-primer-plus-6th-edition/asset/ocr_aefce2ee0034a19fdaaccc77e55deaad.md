# Chapter 5 Loops and Relational Expressions

Other control statements, such as if and while, are treated similarly to for. This serves to visually reinforce the distinction between a control statement and a function call. Also common practice is to indent the body of a for statement to make it stand out.

# Expressions and Statements

A for control section uses three expressions. Within its self-imposed limits of syntax, C++ is a very expressive language. Any value or valid combination of values and operators constitute an expression. For example, 10 is an expression with the value 10 (no surprise), and 28 * 20 is an expression with the value 560. In C++ every expression has a value. Often the value is obvious. For example, the following expression is formed from two values and the addition operator, and it has the value 49:

22 + 27

Sometimes the value is less obvious. For example, the following is an expression because it's formed from two values and the assignment operator:

x = 20

C++ defines the value of an assignment expression to be the value of the member on the left, so the expression has the value 20.The fact that assignment expressions have permits statements such as the following:

maids = (cooks = 4) + 3;

The expression cooks = 4 has the value 4, so maids is assigned the value 7. However, just because C++ permits this behavior doesn't mean you should encourage it. But the same rule that makes this peculiar statement possible also makes the following statement possible:

x = y = z = 0;

This is a fast way to set several variables to the same value.The precedence table (see Appendix D,"Operator Precedence") reveals that assignment associates right-to-left, so first 0 is assigned to z, and then z = 0 is assigned to y, and so on.

Finally, mentioned previously, expressions such as x < y evaluate the bool values true or false.The short program in Listing 5.3 illustrates some points about expression values.The << operator has higher precedence than the operators used in the expressions, so the code uses parentheses to enforce the correct order.

# Listing 5.3 express.cpp

```
// express.cpp -- values of expressions
#include <iostream>
int main()
{
  using namespace std;
  int x;

  cout << "The expression x = 100 has the value ";
```