
Let's put character * that satisfy this logical condition (row+col ==6) && (row<=3 && col>=3) and removing the other (row, col) value pairs.

|  | col=1 | col=2 | col=3 | col=4 | col=5 |
|---|---|---|---|---|---|
| row=1 | 1,1* | 1,2 | 1,3 | 1,4 | 1,5* |
| row=2 | 2,1* | 2,2* | 2,3 | 2,4* | 2,5* |
| row=3 | 3,1* | 3,2 | 3,3* | 3,4 | 3,5* |
| row=4 | 4,1* | 4,2 | 4,3 | 4,4 | 4,5* |
| row=5 | 5,1* | 5,2 | 5,3 | 5,4 | 5,5* |
| row=6 | 6,1* | 6,2 | 6,3 | 6,4 | 6,5* |
| row=7 | 7,1* | 7,2 | 7,3 | 7,4 | 7,5* |

|  | col=1 | col=2 | col=3 | col=4 | col=5 |
|---|---|---|---|---|---|
| row=1 | 1,1* |  |  |  | 1,5* |
| row=2 | 2,1* | 2,2* |  | 2,4* | 2,5* |
| row=3 | 3,1* |  | 3,3* |  | 3,5* |
| row=4 | 4,1* |  |  |  | 4,5* |
| row=5 | 5,1* |  |  |  | 5,5* |
| row=6 | 6,1* |  |  |  | 6,5* |
| row=7 | 7,1* |  |  |  | 7,5* |

The complete selection of boxes now can be expressed by logical condition

```
(col==1) || (col==5) ||

( (row==col) &&( row <=3 && col<=3) ) ||

( (row+col ==6) &&(row<=3 && col>=3) )
```

In the logical condition ( (row==col) &&( row <=3 && col<=3) ), due to logical condition (row==col) the part of the condition given by ( row <=3 && col<=3) is either row<=3 or col<=3 is enough.

This could be further given by

```
( ( row==col ) && row <=3 ) or ( ( row == col ) && col<=3 ).
```

In the logical condition (row+col ==6) &&(row<=3 && col>=3) , every (row, col) value pair in (row+col==6) are given by (5, 1), (4, 2), (3, 3), (2, 4), (1, 5).

| (row, col) value pair | row value | col value |
|---|---|---|
| (1, 5) | 1 | 5 |
| (2, 4) | 2 | 4 |
| (3, 3) | 3 | 3 |
| (4, 2) | 4 | 2 |
| (5, 1) | 5 | 1 |

Every row value is unique within their group of values and is similar with the case for col values too. Hence, considering either row value or col value is sufficient. It is not necessary to consider both the values of row and col to apply restriction condition as given by &&(row <=3 && col>=3).

So part of total logical condition which is given by (row <=3 && col>=3), considering either row<=3 or col>=3 is enough. This could be further given by

```
((row+col ==6 && row <=3 ) or ((row+col ==6 && col>=3 ).
```

We can rewrite the actual logical condition as;

```
(col==1)||(col==5)||
((row==col)&& row <=3)||
( row+col ==6 && row <=3 )
```

Please notice the restriction condition &&row <=3 is same for both logical condition expressions.

We can can again rewrite logical condition in more compact form and can be given as follows:

```
(col==1)||(col==5)||
( ( ( row==col)||( row+col ==6) ) && row<=3 )
```

## Problem YBM1

Change the following logical condition so that we should able to get following output.

```
(col==1)||(col==5)||
( (row==col)&&( row <=3 && col<3) )||
( (row+col ==6) &&(row<=3 && col>=3) )
```

```
*
*   *
*       *
*   *
*
*
*
```

## Problem YBM2

Change the following logical condition so that we should able to get following output.

```
(col==1)||(col==5)||
( (row==col)&&( row <=3 && col<3) )||
( (row+col ==6) &&(row<=3 && col>=3) )
```

```
*               *
*   *       *   *
*       *
*   *       *   *
*               *
*               *
*               *
```

## Problem YBM3

Change the following logical condition so that we should able to get following output.

```
(col==1) || (col==5) ||
((row==col) &&( row <=3 && col<=3 )) ||
((row+col ==6) &&(row<=3 && col>=3 ))
```

```
*               *
    *     *
        *
    *   *
*     *     *
        *
        *
```

## Problem YBM4

Change the following logical condition so that we should able to get following output.

```
(col==1) || (col==5) ||
((row==col) &&( row <=3 && col<=3 )) ||
((row+col ==6) &&(row<=3 && col>=3 ))
```

```
*     *     *
    *   *   *
*   *   *   *
        *
*           *
        *
        *
```

## Problem YBM5

Write logical condition for the following Bluetooth like symbol.

![](img/67765455776ddeb6395161cd553ecd87_66_0.png)

[Hint]

|  | col=1 | col=2 | col=3 | col=4 | col=5 |
|---|---|---|---|---|---|
| row=1 |  |  | 1,3* |  |  |
| row=2 |  |  | 2,3* | 2,4* |  |
| row=3 | 3,1* |  | 3,3* |  | 3,5* |
| row=4 |  | 4,2* | 4,3* | 4,4* |  |
| row=5 |  |  | 5,3* |  |  |
| row=6 |  | 6,2* | 6,3* | 6,4* |  |
| row=7 | 7,1* |  | 7,3* |  | 7,5* |
| row=8 |  |  | 8,3* | 8,4* |  |
| row=9 |  |  | 9,3* |  |  |

## Problem YBN

Write logical condition for Alphabet N to be fit in 7X5 box.

![](img/67765455776ddeb6395161cd553ecd87_66_1.png)

## Problem YBP

Write logical condition for Alphabet P to be fit in 7X5 box.

```
    *   *   *   *
    *           *
    *           *
    *   *   *   *
    *
    *
    *
```

## Problem YBP

Write logical condition for Alphabet R to be fit in 7X5 box.

```
*   *   *   *
    *       *
    *       *
    *   *   *
    *   *
    *       *
    *           *
```

## Problem YBP

Write logical condition for Alphabet S to be fit in 7X5 box.

```
*   *   *   *   *
*   *
*   *
*   *   *   *   *
            *
*   *   *   *   *
*   *   *   *   *
```

## Decision making

There are only two perfect answers in this world either YES or NO. In programming these perfect answers are represented by boolean data type. The boolean data type can take only single value at a time which is either true or false. So boolean value true is represented by YES and boolean value false is represented by NO. While running the program, the control of program may find logical expression. This logical expression is then evaluated to find the result. The result is expressed in terms of either true or false. Based on the boolean result of logical expression the control of program decides whether to execute bunch of programming statements or bypass it.

Such kind of decision making has to be programmed by using following different versions of decision making if-statements.

- a) If-statement
- b) If-else statement
- c) If-else if ...statement (Also known as ladder if-else statement)

Flow-chart helps to visualize the flow of control when condition becomes either true or false.

### a) if-statement

![](img/67765455776ddeb6395161cd553ecd87_68_0.png)

The general syntax for if-statement can be given as:

```
If (condition) {
    execute statement(s);
}
next statement(s); // continue program execution
```

- condition: It will be an expression consisting of variables and operators in such a way so that whose outcome should be a boolean value either true or false. Since logical and comparison operators gives result in either true or false and commonly used in conditional expression.
- When the result of condition is true, it will execute statement(s) enclosed in the If-block {...}.

Note: - A block is placed in a program in order to group set of statement(s) by enclosing it in open curly brace and closed curly brace. An example as follows:

```
{
    statement(s);
}
```

### Case 1

int ageOfCitizen = 80;

condition: (ageOfCitizen >= 60) will evaluate to “true”

So, if (80 >= 60) or if (condition) will be “true” and executes the if-block.

![](img/67765455776ddeb6395161cd553ecd87_69_0.png)

### StatementIf.c

```
#include <stdio.h>

int main() {
    int ageOfCitizen = 80;
    if( ageOfCitizen >= 60 ) {
        printf("Age group - Senior Citizens.");
    }

    return 0;
}
```

### Output

Age group - Senior Citizens.

### Case 2. Change the value of ageOfCitizen in the program

int ageOfCitizen = 40;

condition: (ageOfCitizen >= 60)

if (40 >= 60) will evaluate to "false"

if (condition) will be "false" and it will not execute the if-block.

The output will be blank.

![](img/67765455776ddeb6395161cd553ecd87_70_0.png)

**StatementIf1.c**

```c
#include <stdio.h>

int main() {

    int ageOfCitizen = 40;

    if( ageOfCitizen >= 60 ) {
        printf("Age group - Senior Citizens.");
    }

    return 0;
}
```

> Output

It didn't print anything, since condition becomes failed and code block within if-statement doesn't get executed.

### b) if-else statement

![](img/67765455776ddeb6395161cd553ecd87_71_0.png)

The general syntax for if-else statement can be given as:

```
If (condition) {
    execute statement(s)-1;
} else {
    execute statement(s)-2;
}
next statement(s); // continue program execution
```

If-block

else-block
