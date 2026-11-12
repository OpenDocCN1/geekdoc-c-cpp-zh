Another idea that you should be familiar with in some form is the idea of operator **precedence**. The precedence of an operator determines (1) to which operator an operand belongs and (2) the order in which it will be evaluated in an expression. The inside cover of the text book has a list of the **order of precedence** for the C language.

# Printing Expression Evaluations:

| |
|---|
| `int a = 17; //FIRST OPERAND`<br>`int b = 5; //SECOND OPERAND`<br><br>`printf( "%d + %d = %d\\n", a, b, a + b );`<br><br>`printf( "%d / %d = %d\\n", a, b, a / b );`<br><br>`printf( "%d %% %d = %d\\n", a, b, a % b );` |
| |

Why are there two % characters in the format string of the third printf?

+   * Because the % already has a special meaning in the format string of a printf it takes two to display one to the screen.

> Note: Both operands of the modulus operator must be integral types.

# Assignment Expressions

An assignment expression evaluates the operand on the right side of the assignment operator (=) and saves that value in the memory of the variable on the left.

> Note: The left operand in an assignment expression must be a single variable.

# Examples of Simple Assignment

| |
|---|
| `int x;`<br>`int y = 2;`<br><br>`x = 3 * 4;`<br>`y = y * 3;`<br>`x = x + y;` | Course Standard: Place a space between your operators and operands! |

# Examples of Compound Assignment

+   * It is common to add (or apply another common mathematical operation to) a value to a variable and store that new value back to the variable.