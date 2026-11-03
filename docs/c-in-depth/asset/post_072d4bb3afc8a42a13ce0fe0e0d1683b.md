
++x is equivalent to    x = x + 1
--x is equivalent to    x = x - 1

These operators should be used only with variables; they can't be used with constants or expressions. For example the expressions ++5 or ++(x+y+z) are invalid.

These operators are of two types-
- 1. Prefix increment / decrement – operator is written before the operand (e.g. ++x or --x)
- 2. Postfix increment / decrement – operator is written after the operand (e.g. x++ or x--)

### 4.6.1 Prefix Increment / Decrement

Here first the value of variable is incremented / decremented then the new value is used in the operation

Let us take a variable x whose value is 3.

The statement y = ++x; means first increment the value of x by 1, then assign the value of x to y

This single statement is equivalent to these two statements-
x = x+1;
y = x;

Hence now value of x is 4 and value of y is 4.

The statement y = -- x; means first decrement the value of x by 1 then assign the value of x to y

This statement is equivalent to these two statements.
x = x-1;
y = x;

Hence now value of x is 3 and value of y is 3.

```
/*P4.3 Program to understand the use of prefix increment / decrement */
#include<stdio.h>
main()
{
int x=8;
printf("x = %d\t",x);
printf("x = %d\t",++x); /*prefix increment*/
printf("x = %d\t",--x); /*prefix decrement*/
printf("x = %d\n",x);
}
```

Output:

x = 8    x = 9   x = 9   x = 8   x = 8

In the second printf statement, first the value of x is incremented and then printed; similarly in the fourth printf statement first the value of x is decremented and then printed.

### 4.6.2 Postfix Increment / Decrement

Here first the value of variable is used in the operation and then increment/decrement is performed

Let us take a variable x whose value is 3.

The statement y = x++; means first the value of x is assigned to y and then x is incremented. This statement is equivalent to these two statements-

y = x;
x = x+1;
Hence now value of x is 4 and value of y is 3.

Hence y = x--; means first value of x is assigned to y and then x is decremented.
This statement is equivalent to these two statements-
y = x;
x = x-1;
Hence now value of x is 3 and value of y is 4.

```
/*P4.4 Program to understand the use of postfix increment/decrement*/
#include<stdio.h>
main()
{
 int x=8;
 printf("x = %d\n",x);
 printf("x = %d\n",x++); /*postfix increment*/
 printf("x = %d\n",x);
 printf("x = %d\n",x--); /*postfix decrement*/
 printf("x = %d\n",x);
}
```

Output:
 x = 8 x = 8 x = 9 x = 9 x = 8
In the second printf statement, first the value of x is printed and then incremented; similarly in the fourth printf statement first the value of x is printed and then decremented.

## 4.7 Relational Operators

Relational operators are used to compare values of two expressions depending on their relations. An expression that contains relational operators is called relational expression. If the relation is true then the value of relational expression is 1 and if the relation is false then the value of expression is 0. The relational operators are-

| Operator | Meaning |
| --- | --- |
| < | less than |
| <= | less than or equal to |
| == | equal to |
| != | Not equal to |
| > | Greater than |
| >= | Greater than or equal to |

Let us take two variables a = 9 and b = 5, and form simple relational expressions with them-

| Expression | Relation | Value of Expression |
|------------|----------|--------------------|
| a < b | False | 0 |
| a <= b | False | 0 |
| a == b | False | 0 |
| a != b | True | 1 |
| a > b | True | 1 |
| a >= b | True | 1 |
| a == 0 | False | 0 |
| b!=0 | True | 1 |
| a>8 | True | 1 |
| 2 > 4 | False | 0 |

The relational operators are generally used in if...else construct and loops. In our next program we’ll use the if statement to illustrate the use of relational operators. The if control statement evaluates an expression, and if this expression is true(non zero) then the next statement is executed, otherwise the next statement is skipped. The details of if statement are discussed in chapter 5. Here we have used it to give you an idea of how the relational operators are used.

```
/*P4.5 Program to understand the use of relational operators*/
#include<stdio.h>
main()
{
int a,b;
printf("Enter values for a and b : ");
scanf("%d%d",&a,&b);
if(a<b)
printf("%d is less than %d\n",a,b);
if(a<=b)
printf("%d is less than or equal to %d\n",a,b);
if(a!=b)
printf("%d is not equal to %d\n",a,b);
if(a>b)
printf("%d is greater than %d\n",a,b);
if(a>=b)
printf("%d is greater than or equal to %d\n",a,b);
}
```

Output:
Enter values for a and b : 12 7
12 is not equal to 7
12 is greater than 7
12 is greater than or equal to 7

It is important to note that the assignment operator(=) and equality operator(==) are entirely different Assignment operator is used for assigning values while equality operator is used to compare the expressions. Beginners generally confuse between the two and use one in the place of another, and this leads to an error difficult to find out. For example if in the above program we use '=' instead of '==', then we'll get wrong output.

```
if(a = b)
printf("%d is equal to %d\n",a,b);
```

Here a = b is treated as an assignment expression, so the value of b is assigned to variable a, and the value of the whole expression becomes 7 which is non-zero, and so the next statement is executed.

## 4.8 Logical Or Boolean Operators

An expression that combines two or more expressions is termed as a logical expression. For combining these expressions we use logical operators. These operators return 0 for false and 1 for true. The operands may be constants, variables or expressions. C has three logical operators.

| Operator | Meaning |
|---|---|
| && | AND |
| || | OR |
| ! | NOT |

Here logical NOT is a unary operator while the other two are binary operators. Before studying these operators let us understand the concept of true and false. In C any non-zero value is regarded as true and zero is regarded as false.

### 4.8.1 AND ( && ) Operator

This operator gives the net result true if both the conditions are true, otherwise the result is false.

### Boolean Table

| Condition1 | Condition2 | Result |
|---|---|---|
| False | False | False |
| False | True | False |
| True | False | False |
| True | True | True |

Let us take three variables a = 10, b = 5, c = 0

Suppose we have a logical expression-
(a == 10) && (b < a)

Here both the conditions a == 10 and b < a are true, and hence this whole expression is true. Since the logical operators return 1 for true hence the value of this expression is 1.

| Expression |  | Result | Value of expression |
|---|---|---|---|
| (a ==10) && (b>a) | true && false | false | 0 |
| (b>=a) && (b==3) | false && false | false | 0 |
| a && b | true && true | true | 1 |
| a && c | true && false | false | 0 |

In the last two expressions we have taken only variables. Since nonzero values are regarded as true and zero value is regarded as false, so variables a and b are considered true and variable c is considered false.

### 4.8.2 OR ( || ) Operator

This operator gives the net result false, if both the conditions have the value false, otherwise the result is true.

### Boolean Table

| Condition1 | Condition2 | Result |
|---|---|---|
| False | False | False |
| False | True | True |
| True | False | True |
| True | True | True |

Let us take three variables a = 10, b = 5, c = 0

Consider the logical expression-

```
(a >= b) || (b > 15)
```

This gives result true because one condition is true.

| Expression |  | Result | Value of expression |
|---|---|---|---|
| a || b | true || true | true | 1 |
| a || c | true || false | true | 1 |
| (a<9) || (b>10) | false || false | false | 0 |
| (b!=7) || c | true || false | true | 1 |

### 4.8.3 Not ( ! ) Operator

This is a unary operator and it negates the value of the condition. If the value of the condition is false then it gives the result true. If the value of the condition is true then it gives the result false.

### Boolean Table

| Condition | Result |
|---|---|
| False | True |
| True | False |

Let us take three variables a = 10, b = 5, c = 0
Suppose we have this logical expression-
! ( a == 10 )
The value of the condition (a==10) is true. NOT operator negates the value of the condition. Hence the result is false.
