integer value x as an argument and returns a resultant integer which is the factorial of x. Hence, the prototype of the function `factorial()` will be as follows:

```
int factorial(int);
```

Mathematically speaking, `factorial(x)` is calculated as

`factorial(x) = x* (x−1) * (x−2) * (x−3) ...*1`  
*equation (3)*

The principle of recursion is to conquer a large problem by dividing it into multiple small problems. Hence, we rewrite the expression for `factorial(x)` as

`factorial(x) = x* factorial(x−1);`  
*equation (4)*

This means that the factorial of any number x is multiplication of x with the factorial of the previous number which is (x−1). Actually, equation 4 is formed by substituting (x−1)*(x−2)*(x−3)……. *1 in equation 3 with factorial (x−1) because this expression is indeed factorial of x−1.

To understand the calculation of factorial using recursion, let us assume x = 4. Factorial of 4 can be calculated as

```
factorial(4) = 4* factorial(3);
```

This means that we must calculate the factorial of 3 before we calculate the factorial of 4. We can further split the calculation of factorial(3) as shown below:

```
factorial(3) = 3* factorial(2);
```

We can continue this process until we reach a stage where no further split is possible. This means that we continue the splitting until we reach an expression:

```
factorial(1) = 1* factorial(0);
```

There is no point in dividing the term `factorial(0)` because we know that 0! is always 1. Hence, this is a stage where we terminate the recursion.

> **NOTES**
> 
> In general, `factorial(x)` when `x > 0` is calculated as
> 
> `factorial(x) = x* factorial(x−1);`
> 
> We know that zero factorial is 1. Hence, x=0 is a condition that can be used to terminate recursion.

Given below is the source code of the function to calculate the factorial of a number x.

```
#include<stdio.h>
int factorial(int);
void main()
{
int x,y,res;
printf("Enter the value of x\n");
```