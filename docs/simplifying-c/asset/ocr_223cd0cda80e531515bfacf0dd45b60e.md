```
area = (base * height)/2;
roll_no = 14;
```

In the first example, an expression is assigned to the variable area, while the second example assigns a constant value 14 to the variable roll_no. Note that the left operand of the assignment statement has to be a single variable.

The special symbol = is also used as a shorthand operator. The shorthand operator is used to reduce the size of expressions and improve the readability of C programs. To convert the special symbol = into a shorthand operator, we prefix any arithmetic operator to =. The syntax of a shorthand operator is as follows:

```
identifier AOp= expression; or identifier AOp= constant value;
```

where the identifier is any valid variable name, AOp refers to an arithmetic operator, and AOp= is a shorthand operator. Some examples of the shorthand operators are as follows:

```
counter += 1;
table *= 2;
first /= (second + third);
```

The statement counter += 1; is equivalent to counter = counter + 1; while table *= 2; is equivalent to table = table * 2; and first /= (second + third); is equivalent to first = first / (second + third). It can be observed from these examples that if a variable appears on both the left-hand side (LHS) and right-hand side (RHS), then we can use the shorthand operator in such expressions. The expression built by using shorthand operator is known as a compound assignment statement. If a compound assignment contains a binary expression, as shown in example 3, the binary expression will always be resolved first. With certain amount of practice, shorthand operators can become an efficient tool to improve the readability of C programs. Program 6 illustrates the usage of shorthand operators:

# Program 6

```
/* Program to illustrate the use of shorthand operator */
#include <stdio.h>
/* Beginning of main function */
main()
{
/* Declaration of an integer variables */
int i_number, i_const;

/* Accept the value of number*/
printf("\n Enter the value of number: ");
scanf("%d",&i_number);
printf("\n Enter the value of constant: ");
scanf("%d",&i_const);

/* Print value of number */
printf("\n Initial value of i_number: %d", i_number);

/* Use of shorthand operator */
i_number += i_const;
```