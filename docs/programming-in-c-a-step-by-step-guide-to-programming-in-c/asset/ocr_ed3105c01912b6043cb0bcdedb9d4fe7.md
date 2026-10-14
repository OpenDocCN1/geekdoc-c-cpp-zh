# 5.7 Terminal Questions

+   1. What is the significance of the keyword ‘void’?
+   2. What is the difference between function declaration and function definition?
+   3. Write a recursive function to find sum of even numbers from 2 to 10.
+   4. Write a recursive definition to find gcd of two numbers.
+   5. Write a recursive definition to find nth fibonacci number. The Fibonacci series forms a sequence of numbers in which each number is equal to the sum of the previous two numbers. In other words,

$F_i=F_{i-1}+F_{i-2}$

where F refers to the ith Fibonacci number. The first two Fibonacci numbers are 0 and 1, i.e, F1=0, F2=1;

6. What is the output of the following program?

```
```c
#include<stdio.h>
main()
{
int m, count;
int fun(int count);
for(count=1;count<=10;count++) {
m=fun(count);
printf("%d",m);
}
}
```
```