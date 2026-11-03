
```
c2=i1;    /*Demotion : int converted to char*/
i2=f1;    /*Demotion : float converted to int*/
/*Now c2 has character with ASCII value 80,i2 is assigned value 12*/
printf("c2 = %c,  i2 = %d\n",c2,i2);
f2=i1;    /*Promotion : int converted to float*/
i2=c1;    /*Promotion : char converted to int*/
/*Now i2 contains ASCII value of character 'H' which is 72*/
printf("f2 = %.2f,  i2 = %d\n",f2,i2);
}
```

Output:
 c2 = P,   i2 = 12
 f2 = 80.00, i2 = 72

## 4.12.4 Explicit Type Conversion Or Type Casting

There may be certain situations where implicit conversions may not solve our purpose. For example-

```
float z;
int x = 20, y = 3;
z = x/y;
```

The value of z will be 6.0 instead of 6.66.

In these types of cases we can specify our own conversions known as type casting or coercion. This is done with the help of cast operator. The cast operator is a unary operator that is used for converting an expression to a particular data type temporarily. The expression can be any constant or variable

The syntax of cast operator is-
(datatype) expression
Here the datatype along with the parentheses is called the cast operator.
So if we write the above statement as-
z = (float)x/y;
Now the value of z will come out to be 6.66. This happens because the cast operator (float) temporarily converted the int variable x into float type and so floating point arithmetic took place and fraction part was not lost.
Note that the cast operator changes the data type of variable x only temporarily for the evaluation of this expression, everywhere else in the program it will be an int variable only.

```
/*P4.11 Program to illustrate the use of cast operator*/
#include<stdio.h>
main()
{
    int x=5,y=2;
    float p,q;
    p=x/y;
    printf("p = %f\n",p);
    q=((float)x)/y;
    printf("q = %f\n",q);
}
```

### Output:

p = 2.000000
q = 2.500000

Initially the expression x/y is evaluated, both x and y are integers so according to integer arithmetic after division, decimal value is truncated and result is integer value 2. This value will be assigned to p, but p is a float variable so according to implicit type conversion in assignment the integer value 2 will be converted to float and then assigned to p. So finally the value of p is 2.0

When cast operator is used, floating point arithmetic is performed hence the value of q is 2.5

Here are some other examples of usage of cast operator-

| Expression | Description |
|---|---|
| (int)20.3 | constant 20.3 converted to integer type and fractional part is lost(Result 20) |
| (float)20/3 | constant 20 converted to float type, and then divided by 3 (Result 6.66) |
| (float)(20/3) | First 20 divided by 3 and then result of whole expression converted to float type(Result 6.00) |
| (double)(x + y -z) | Result of expression x+y-z is converted to double |
| (double)x+y-z | First x is converted to double and then used in expression |

## 4.13 Precedence And Associativity Of Operators

For evaluation of expressions having more than one operator, there are certain precedence and associativity rules defined in C. Let us see what these rules are and why are they required.

Consider the following expression-

```
2 + 3 * 5
```

Here we have two operators- addition and multiplication operators. If addition is performed before multiplication then result will be 25 and if multiplication is performed before addition then the result will be 17.

In C language, operators are grouped together and each group is given a precedence level. The precedence of all the operators is given in the following table. The upper rows in the table have higher precedence and it decreases as we move down the table. Hence the operators with precedence level 1 have highest precedence and with precedence level 15 have lowest precedence. So whenever an expression contains more than one operator, the operator with a higher precedence is evaluated first. For example in the above expression, multiplication will be performed before addition since multiplication operator has higher precedence than the addition operator.

| Operator | Description | Precedence level | Associativity |
|---|---|---|---|
| ( ) | Function call | 1 | Left to Right |
| [ ] | Array subscript | 1 | Left to Right |
| -> | Arrow operator | 1 | Left to Right |
| . | Dot operator | 1 | Left to Right |
| + | Unary plus | 2 | Right to Left |
| - | Unary minus | 2 | Right to Left |
| ++ | Increment | 2 | Right to Left |
| -- | Decrement | 2 | Right to Left |
| ! | Logical NOT | 2 | Right to Left |
| ~ | One's complement | 2 | Right to Left |
| * | Indirection | 2 | Right to Left |
| & | Address | 2 | Right to Left |
| (datatype) | Type cast | 2 | Right to Left |
| sizeof | Size in bytes | 2 | Right to Left |
| * | Multiplication | 3 | Left to Right |
| / | Division | 3 | Left to Right |
| % | Modulus | 3 | Left to Right |
| + | Addition | 4 | Left to Right |
| - | Subtraction | 4 | Left to Right |
| << | Left shift | 5 | Left to Right |
| >> | Right shift | 5 | Left to Right |
| < | Less than | 6 | Left to Right |
| <= | Less than or equal to | 6 | Left to Right |
| > | Greater than | 6 | Left to Right |
| >= | Greater than or equal to | 6 | Left to Right |
| == | Equal to | 7 | Left to Right |
| != | Not equal to | 7 | Left to Right |
| & | Bitwise AND | 8 | Left to Right |
| ^ | Bitwise XOR | 9 | Left to Right |
| \| | Bitwise OR | 10 | Left to Right |
| && | Logical AND | 11 | Left to Right |
| \|\| | Logical OR | 12 | Left to Right |
| ? : | Conditional operator | 13 | Right to Left |
| = | Assignment operators | 14 | Right to Left |
| *= /= %= | Assignment operators | 14 | Right to Left |
| += -= | Assignment operators | 14 | Right to Left |
| &= ^= \|= | Assignment operators | 14 | Right to Left |
| <<= >>= | Assignment operators | 14 | Right to Left |
| , | Comma operator | 15 | Left to Right |

Let us take some expressions and see how they will be evaluated-

(i) x = a+b < c

Here + operator has higher precedence than < and =, and < has more precedence than =, so first a+b will be evaluated, then < operator will be evaluated, and at last the whole value will be assigned to x. If initial values are a = 2, b = 6, c = 9, then final value of x will be 1.

(ii) x *= a + b

Here + operator has higher precedence than *=, so a+b will be evaluated before compound assignment. This is interpreted as x = x*(a+b) and not as x = x*a+b. If initial values are x = 5, a = 2, b = 6, then final value of x will be 13.

(iii) x = a<=b || b==c

Here order of evaluation of operators will be <=, ==, ||. If initial values are a = 2, b = 3, c = 4, then final value of x will be 1.

In the above examples we have considered expressions that contain operators having different precedence levels. Now consider a situation when two operators with the same precedence occur in an expression.

For example-

5 + 16 / 2 * 4

Here / and * have higher precedence than + operator, so they will be evaluated before addition. But / and * have same precedence, so which one of them will be evaluated first still remains a problem. If / is evaluated before *, then the result is 37 otherwise the result is 7. Similarly consider this expression-

20 - 7 - 5 - 2 -1

Here we have four subtraction operators, which of course have the same precedence level. If we decide to evaluate from right to left answer will be 5, and if we evaluate from left to right the answer will be 17.

To solve these types of problems, an associativity property is assigned to each operator. Associativity of the operators within same group is same. All the operators either associate from left to right or from right to left. The associativity of all operators is also given in the precedence table. Now again consider the above two expressions-

5 + 16 / 2 *4

Since / and * operators associate from left to right so / will be evaluated before * and the correct result is 37.

20 - 7 - 5 - 2 -1

The subtraction operator associates from left to right so the value of this expression is 5.

The assignment operator associates from right to left. Suppose we have a multiple assignment expression like this-

x = y = z = 5

Here initially the integer value 5 is assigned to variable z and then value of expression z = 5 is assigned to variable y. The value of expression z = 5 is 5, so 5 is assigned to variable y and now the value of expression y = z = 5 becomes 5. Now value of this expression is assigned to x and the value of whole expression x = y = z = 5 becomes 5.

The conditional operator also associates from right to left. Consider this expression-

x ? y : a ? b : c
