# Note

+   - In the division of one integer by another, the remainder is discarded. Thus, 7/3 is 2, and 9/11 is 0. The % operator can only be used with the integer variables. It cannot be used with the variables of float or double type.
+   - The multiplication, division, and residue-modulo operators have the same priority. The addition and subtraction operators also have equal priority, but this is lower than that of the former three operators, *, /, and %. All these operators group from left to right. In a C program, is the value of 3/5 + 2/5 the same as (3 + 2)/5? Is 3 * (7/5) the same as 3 * 7/5? The answer to both questions is ‘No’.

# EXAMPLES

In the examples below, let x be an integer variable.

+   13. `x = 2 * 3 + 4 * 5;`
+   
+       The products 2 * 3 and 4 * 5 are evaluated first; the sum 6 + 20 is computed next; finally the assignment of 26 is made to x.
+   
+   14. `x = 2 * (3 + 4) * 5;`
+   
+       The parentheses guarantee that 3 + 4 be evaluated first. Since multiplication groups from left to right, the intermediate result 7 will be multiplied by 2 and then by 5, and the assignment of 70 will finally be made to x.
+   
+   15. `x = 7*6 % 15/9;`
+   
+       Each of the operators above has equal priority; each groups from left to right. Therefore, the multiplication 7 * 6 (≡ 42) is done first, then the residue-modulo with respect to 15 (42 % 15 = 12), and finally the division of (12) by 9. Since the division of one integer by another yields the integer part of the quotient and truncates the remainder, 12/9 gives the value 1. x is therefore assigned the value 1.
+   
+   16. `x = 7 * (6 % 15)/9;`
+   
+       The parentheses ensure that 6 % 15 is evaluated first. The remainder, when 6 is divided by 15, is 6. In the second step, this result is multiplied by 7, yielding 42. Integer division of 42 by 9 gives 4 as the quotient, which is the value assigned to x.
+   
+   17. `x = 7*6 % (15/9);`
+   
+       Here, 15/9 is performed first and yields 1. The next computation in order is 7 * 6 % 1, i.e., the remainder, on division of 42 by 1, is 0. x gets the value 0.
+   
+   18. `x = 7 * ((6 % 15)/9);`
+   
+       The innermost parentheses are evaluated first: 6 % 15 is 6. The outer parentheses are evaluated next—6/9 is 0. x gets the value 7 * 0 = 0.
+   
+   19. An example of the use of precedence of operators

```
```c
#include <stdio.h>
int main()
{
    int a;
    int b = 4;

    int c = 8;
    int d = 2;
    int e = 4;
    int f = 2;
    a = b + c / d + e * f;
                /* result without parentheses */
    printf("The value of a is = %d \n", a);
    a = (b + c) / d + e * f;
                /* result with parentheses */
    printf("The value of a is = %d \n", a);
    a = b + c / ((d + e) * f);
                /* another result with parentheses */
    printf("The value of a is = %d \n", a);
    return 0;
}
```
```

**Output**

The value of a is = 16
The value of a is = 14
The value of a is = 4

# 8.14 EXPRESSIONS REVISITED

An expression in C consists of a syntactically valid combination of operators and operands that computes to a value. An expression by itself is not a statement. Remember, a statement is terminated by a semicolon; an expression is not. Expressions may be thought of as the constituent elements of a statement, the ‘building blocks’ from which statements may be constructed. The important thing to note is that every C expression has a value. The number 7 as we said a while ago, or any other number by itself, is also an expression, the value of the number being the value of the expression. For example,

`3 * 4 % 5`

is an expression with value 2.

`x = 3 * 4`

is an example of an assignment expression. Note the absence of the semicolon in the assignment above. The terminating semicolon would have converted the expression into a statement. Like any other C expression, an assignment expression also has a value. Its value is the value of the quantity on the right-hand side of the assignment operator. Consequently, in the present instance, the value of the expression (`x = 3 * 4`) is 12. Consider a C statement such as

`z = (x = 3 * 4) / 5;`

Here, the parentheses ensure that x is assigned the value 12 first. It is also the value of the parenthetical expression (`x = 3 * 4`), from the property that every expression has a value. Thus, the entire expression reduces to

`z = 12/5`

Next, in order of evaluation, the integer division of 12 by 5 yields 2. The leftmost assignment operator finally gives the