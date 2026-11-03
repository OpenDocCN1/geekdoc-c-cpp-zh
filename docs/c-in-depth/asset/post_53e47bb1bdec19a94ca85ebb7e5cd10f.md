
of local variable gets printed.

## 6.18.3 Static Variables

Static variables are declared by writing the keyword `static` in front of the declaration.

```c
static type var_name;
```

A static variable is initialized only once, and the value of a static variable is retained between function calls. If a static variable is not initialized, then it is automatically initialized to 0.

```c
/*P6.23 Program to understand the use of static variables*/
#include<stdio.h>
void func(void);
main()
{
    func();
    func();
    func();
}
void func(void)
{
    int a=10;
    static int b=10;
    printf("a = %d    b = %d\n",a,b);
    a++;
    b++;
}
```

**Output:**

```text
a = 10   b = 10
a = 10   b = 11
a = 10   b = 12
```

Here `b` is a static variable. The first time the function is called, `b` is initialized to 10. Inside the function, the value of `b` becomes 11. This value is retained, and the next time the function is called, the value of `b` is 11 and initialization is neglected. Similarly, the third time the function is called, the value of `b` is 12. Note that the variable `a`, which is not static, is initialized on each call and its value is not retained.

## 6.19 Recursion

Recursion is a powerful technique for writing a complicated algorithm in an easy way. According to this technique, a problem is defined in terms of itself. The problem is solved by dividing it into small problems that are similar in nature to the original problem. These smaller problems are solved, and their solutions are applied to get the final solution to the original problem.

To implement recursion in programming, a function should be capable of calling itself. This facility is available in C. A function that calls itself (inside its function body) again and again is known as a recursive function. In recursion, the calling function and the called function are the same. For example:

```c
main()
{
    ......
    rec();
    ......
}
rec()
{
    ......
    rec();   // recursive call
    ......
}
```

Here `rec()` is called inside the body of the function `rec()`. There should be a terminating condition to stop recursion; otherwise, `rec()` will keep on calling itself infinitely and will never return.

```c
rec()
{
    if(...) /*terminating condition*/
    .....
    rec();
}
```

Before writing a recursive function for a problem, we should consider these points:

1. We should be able to define the solution to the problem in terms of a similar, smaller problem. At each step, we get closer to the final solution to the original problem.
2. There should be a terminating condition to stop recursion.

Now we will take some problems and write recursive functions for solving them:

- (i) Factorial
- (ii) Power
- (iii) Fibonacci numbers
- (iv) Tower of Hanoi

We know that the factorial of a positive integer `n` can be found by multiplying all integers from 1 to `n`.

`n! = 1 * 2 * 3 * ........ * (n-1) * n`

This is the iterative definition of factorial, and in the previous chapter we had written a program to compute factorial using a loop. Now we'll try to find out the recursive definition of factorial.

We know that `6! = 6*5*4*3*2*1`. We can write it as `6! = 6 * 5!`. Similarly, we can write `5! = 5*4!`. So, in general, we can write `n! = n * (n-1)!`.

Now the problem of finding the factorial of `(n-1)` is similar to that of finding the factorial of `n`, but it is definitely smaller in size. So we have defined the solution of the factorial problem in terms of itself. We know that the factorial of 0 is 1. This can act as the terminating condition. So the recursive definition of factorial can be written as:

```text
n! = { 1          n=0
      n * (n-1)!   n>0 }
```

Now we'll write a program that finds the factorial using a recursive function.

```c
/*P6.24 Program to find the factorial of a number by recursive method*/
#include<stdio.h>
long fact(int n);
main()
{
    int num;
    printf("Enter a number : ");
    scanf("%d",&num);
    printf("Factorial of %d is %ld\n",num,fact(num));
}
long fact(int n)
{
    if (n==0)
        return(1);
    else
        return(n*fact(n-1));
}
```

This function returns 1 if the argument `n` is 0; otherwise, it returns `n*fact(n-1)`. To return `n*fact(n-1)`, the value of `fact(n-1)` has to be calculated, for which `fact()` has to be called again, this time with an argument of `n-1`. This process of calling `fact()` continues until it is called with an argument of 0.

Suppose we want to find the factorial of 5:

- Initially, `main()` calls `factorial(5)`.
- Since 5 > 0, `factorial(5)` calls `factorial(4)`.
- Since 4 > 0, `factorial(4)` calls `factorial(3)`.
- Since 3 > 0, `factorial(3)` calls `factorial(2)`.
- Since 2 > 0, `factorial(2)` calls `factorial(1)`.
- Since 1 > 0, `factorial(1)` calls `factorial(0)`.

**Winding phase**

When `factorial()` is called with `n=0`, the condition inside the `if` statement becomes true, so recursion stops and control returns to `factorial(1)`. Now every called function returns its value to the previous function. These values are returned in the reverse order of function calls.

Recursive functions work in two phases. The first is the winding phase, and the next is the unwinding phase. In the winding phase, the function keeps calling itself. The winding phase stops when the terminating condition is reached in a call. Then the unwinding phase starts, and the called functions return values in reverse order.

In the above case, the function `factorial()` is called 6 times, but there is only one copy of that function in memory. Each function call is different from another because the argument supplied is different each time.

Now we'll write a recursive function for finding `a^n`.

The iterative definition for finding `a^n` is:

`a^n = a * a * a ........... n times`

The recursive definition can be written as:

```text
a^n = { 1          n=0
        a * a^(n-1)  n>0 }
```

```c
/*P6.25 Program to raise a floating point number to a positive integer using recursion*/
#include<stdio.h>
float power(float a,int n);
main()
{
    float a,p;
    int n;
    printf("Enter a and n : ");
    scanf("%f%d",&a,&n);
    p=power(a,n);
    printf("%f raised to power %d is %f\n",a,n,p);
}
float power(float a,int n)
{
    if(n==0)
        return(1);
    else
        return(a*power(a,n-1));
}
```

In P5.20, we had written a program to print the Fibonacci series. Now we'll write a recursive definition for finding Fibonacci numbers.

```text
fib(n) = { 1                     n=0 or n=1
           fib(n-1)+fib(n-2)    n>1 }
```

```c
/*P6.26 Program to generate Fibonacci series using recursion*/
#include<stdio.h>
```

## For n=1

![](img/a76c706396af8b310f291a5313a27079_151_0.png)

S→D means move the disk from pillar S to pillar D.

## For n=2

![](img/a76c706396af8b310f291a5313a27079_151_1.png)

- (i) Move disk 1 from pillar S to T (S→T)
- (ii) Move disk 2 from pillar S to D (S→D)
- (iii) Move disk 1 from pillar T to D (T→D)

## For n=3

![](img/a76c706396af8b310f291a5313a27079_151_2.png)

- (i) Move disk 1 from pillar S to D (S→D)
- (ii) Move disk 2 from pillar S to T (S→T)
- (iii) Move disk 1 from pillar D to T (D→T)
- (iv) Move disk 3 from pillar S to D (S→D)
- (v) Move disk 1 from pillar T to S (T→S)
- (vi) Move disk 2 from pillar T to D (T→D)
- (vii) Move disk 1 from pillar S to D (S→D)

These were the solutions for n=1, n=2, and n=3. From these solutions, we can observe that first we move n-1 disks from the source pillar (S) to the temporary pillar (T), and then move the largest disk to the destination pillar (D). So the general solution for n disks can be written as:

1. Move the upper n-1 disks from S to T.
2. Move the nth disk from S to D.
3. Move n-1 disks from T to D.

To move n-1 disks from S to T, we can use D as the temporary pillar, and to move n-1 disks from T to D, we can use S as the temporary pillar.

```text
tofh(n, source, temp, dest) =

Move disk from source to dest    n=1
tofh(n-1, source, dest, temp)
Move nth disk from source to dest    n>1
tofh(n-1, temp, source, dest)
```

```c
/*P6.27 Program to solve Tower of Hanoi problem using recursion*/
#include<stdio.h>
main()
{
    char source='S',temp='T',dest='D';
    int ndisk;
    printf("Enter the number of disks : ");
    scanf("%d",&ndisk);
    printf("Sequence is :\n");
    tofh(ndisk,source,temp,dest);
}
tofh(int ndisk,char source,char temp,char dest)
{
    if(ndisk>0)
    {
        tofh(ndisk-1,source,dest,temp);
        printf("Move Disk %d %c->%c\n",ndisk,source,dest);
        tofh(ndisk-1,temp,source,dest);
    }
}/*End of tofh()*/
```
