
## Assigning values

![](img/d1dfb0563339ba187decb78799155b7f_55_0.png)

The operators that are used in C programs to assign values are listed in the table below. All except the simple = assign operator are a shorthand form of a longer expression, so each equivalent is given for clarity.

| Operator: | Example: | Equivalent: |
|---|---|---|
| = | a = b | a = b |
| += | a += b | a = ( a + b ) |
| -= | a -= b | a = ( a - b ) |
| *= | a *= b | a = ( a * b ) |
| /= | a /= b | a = ( a / b ) |
| %= | a %= b | a = ( a % b ) |

It is important to regard the = operator to mean “assign” rather than “equals” to avoid confusion with the == equality operator.

In the example above, the variable named a is assigned the value that is contained in the variable named b – so that becomes the new value stored in the a variable.

The += operator is useful to add a value onto an existing value that is stored in the a variable. In the table example, the += operator first adds the value stored in the variable a to the value stored in the variable b. It then assigns the result to become the new value stored in the a variable.

All the other operators in the table work in the same way by making the arithmetical operation between the two values first, then assigning the result to the first variable to become its new stored value.

With the %= operator, the first operand a is divided by the second operand b, then the remainder of the operation is assigned to the a variable.

![](img/d1dfb0563339ba187decb78799155b7f_55_1.png)

> The == equality operator compares operand values. This is described on page 56.

- Begin a new program with a preprocessor instruction to include the standard input/output library functions #include <stdio.h>

- Add a main function that declares two integer variables

```
int main()
{
  int a , b;
}
```

- Next, in the main function block, output the result of assignment operations performed on the variables

```
printf("Assigned:\n");
printf("\tVariable a = %d\n", a = 8);
printf("\tVariable b = %d\n", b = 4);
printf("Added & assigned:\n");
printf("\tVariable a += b (8+=4) a = %d\n", a += b);
printf("Subtracted & assigned:\n");
printf("\tVariable a-=b (12-=4) a = %d\n", a -= b);
printf("Multiplied & assigned:\n");
printf("\tVariable a*=b (8*=4) a = %d\n", a *= b);
printf("Divided & assigned:\n");
printf("\tVariable a/=b (32/=4) a = %d\n", a /= b);
printf("Modulo & assigned:\n");
printf("\tVariable a%%=b (8%%=4) a = %d\n", a %= b);
```

- At the end of the main function block, return a zero integer value, as required by the function declaration

```
return 0;
```

- Save the program file, then compile and execute the program to see the results of the assignment operations

![](img/d1dfb0563339ba187decb78799155b7f_56_0.png)

![](img/d1dfb0563339ba187decb78799155b7f_56_1.png)

Notice that %% must be used in order to display the % character with the printf() function.

![](img/d1dfb0563339ba187decb78799155b7f_56_2.png)

## Comparing values

The operators that are commonly used in C programming to compare two numerical values are listed in the table below:

| Operator: | Comparative test |
|---|---|
| == | Equality |
| != | Inequality |
| > | Greater than |
| < | Less than |
| >= | Greater than or equal to |
| <= | Less than or equal to |

The == equality operator compares two operands and will return 1 (true) if both are equal in value, otherwise it will return 0 (false). If both are the same number they are equal, or if both are characters their ASCII code value is compared numerically.

Conversely, the != inequality operator returns 1 (true) if the two operands are not equal, using the same rules as the == equality operator; otherwise it returns 0 (false).

Equality and inequality operators are useful in testing the state of two variables to perform conditional branching in a program.

The > "greater than" operator compares two operands and will return 1 (true) if the first is greater in value than the second, or it will return 0 (false) if it is equal or less in value. The > "greater than" operator is frequently used to test the value of a countdown value in a loop.

The < "less than" operator makes the same comparison but returns 1 (true) if the first operand is less in value than the second, otherwise it returns 0 (false).

Adding the = operator after a > "greater than" or < "less than" operator makes it also return 1 (true) when the two operands are exactly equal in value.

Further information on ASCII code values can be found in the Reference section on pages 162-163.

![](img/d1dfb0563339ba187decb78799155b7f_57_0.png)

![](img/d1dfb0563339ba187decb78799155b7f_57_1.png)

- Begin a new program with a preprocessor instruction to include the standard input/output library functions

```c
#include <stdio.h>
```

- Add a main function that declares and initializes three integer variables and two character variables

```c
int main()
{
    int zero = 0 , nil = 0 , one = 1 ;
    char upr = 'A' , lwr = 'a' ;
}
```

- Next, in the main function block, output the result of comparison operations performed on the variables

```c
printf( "Equality (0==0): %d \n" , zero == nil );
printf( "Equality (0==1): %d \n" , zero == one );
printf( "Equality (A==a): %d \n" , upr == lwr );
printf( "Inequality (A!=a): %d \n" , upr != lwr );
printf( "Greater than (1>0): %d \n" , one > nil );
printf( "Less than (1<0): %d \n" , one < nil );
printf( "Greater or equal (0>=0): %d \n" , zero >= nil );
printf( "Less or equal (1<=0): %d \n" , one <= nil );
```

- At the end of the main function block, return a zero integer value, as required by the function declaration

```c
return 0 ;
```

- Save the program file, then compile and execute the program to see the results of the comparison operations

![](img/d1dfb0563339ba187decb78799155b7f_58_0.png)

> **Don't forget:** Numerically, 1 represents a true result and 0 represents a false result.

> **Hot tip:** The ASCII code value for uppercase 'A' is 65 and for lowercase 'a' it's 97 — so their comparison here returns 0 (false).

![](img/d1dfb0563339ba187decb78799155b7f_58_1.png)

## Assessing logic

The logical operators most commonly used in C programming are listed in the table below:

| Operator: | Operation: |
|---|---|
| && | Logical AND |
| || | Logical OR |
| ! | Logical NOT |

The logical operators are used with operands that have the Boolean values of true or false, or an expression that can convert to true or false.

The logical && AND operator will evaluate two operands and return true only if both operands are themselves true. Otherwise, the && AND operator will return false.

This is used in conditional branching, where the direction of a C program is determined by testing two conditions. If both conditions are satisfied, the program will go in a certain direction, otherwise it will take a different direction.

Unlike the && AND operator that needs both operands to be true, the || OR operator will evaluate two operands and return true if either one of the operands is itself true. If neither operand is true then the || OR operator will return false. This is useful in C programming to perform a certain action if either one of two test conditions has been met.

![](img/d1dfb0563339ba187decb78799155b7f_59_0.png)

The term "Boolean" refers to a system of logical thought developed by the English mathematician George Boole (1815-1864).

The third logical ! NOT operator is a "unary" operator – that is used before a single operand. It returns the inverse value of the given operand, so if the variable var is a true value then !var would return a false value. The ! NOT operator is useful in C programming to toggle the value of a variable in successive loop iterations with a statement like var = !var. This ensures that on each pass the value is reversed, like flicking a light switch on and off.

In C programming, a zero represents the Boolean false value; and any non-zero value, such as 1, represents the Boolean true value.
