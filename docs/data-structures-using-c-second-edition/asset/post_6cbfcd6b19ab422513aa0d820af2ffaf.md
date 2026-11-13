
factorial of a number. Every recursive function must have a base case and a recursive case. For the factorial function,

### Programming Tip

Every recursive function must have at least one base case. Otherwise, the recursive function will generate an infinite sequence of calls, thereby resulting in an error condition known as an infinite stack.

- Base case is when n = 1, because if n = 1, the result will be 1 as 1! = 1.
- Recursive case of the factorial function will call itself but with a smaller value of n, this case can be given as
  factorial(n) = n x factorial(n-1)

Looking at the above program which calculates the factorial of a number recursively.

## Programming Example

### 10. Write a program to calculate the factorial of a given number.

```c
#include <stdio.h>
int Fact(int); // FUNCTION DECLARATION
int main()
{
    int num, val;
    printf("\n Enter the number: ");
    scanf("%d", &num);
    val = Fact(num);
    printf("\n Factorial of %d = %d", num, val);
    return 0;
}
int Fact(int n)
{
    if(n==1)
    return 1;
    else
    return (n * Fact(n-1));
}
```

Output
Enter the number : 5
Factorial of 5 = 120

From the above example, let us analyse the steps of a recursive program.

- Step 1: Specify the base case which will stop the function from making a call to itself.
- Step 2: Check to see whether the current value being processed matches with the value of the base case. If yes, process and return the value.
- Step 3: Divide the problem into smaller or simpler sub-problems.
- Step 4: Call the function from each sub-problem.
- Step 5: Combine the results of the sub-problems.
- Step 6: Return the result of the entire problem.

## Greatest Common Divisor

The greatest common divisor of two numbers (integers) is the largest integer that divides both the numbers. We can find the GCD of two numbers recursively by using the Euclid's algorithm that states

```
GCD (a, b) = | b, if b divides a |
             | GCD (b, a mod b), otherwise
```

GCD can be implemented as a recursive function because if b does not divide a, then we call the same function (GCD) with another set of parameters that are smaller than the original ones. Here we assume that a > b. However if a < b, then interchange a and b in the formula given above.

### Working

```
Assume a = 62 and b = 8
GCD(62, 8)
rem = 62 % 8 = 6
GCD(8, 6)
rem = 8 % 6 = 2
GCD(6, 2)
rem = 6 % 2 = 0
Return 2
Return 2
Return 2
```

## PROGRAMMING EXAMPLE

### 11. Write a program to calculate the GCD of two numbers using recursive functions.

```c
#include <stdio.h>
int GCD(int, int);
int main()
{
    int num1, num2, res;
    printf("\n Enter the two numbers : ");
    scanf("%d %d", &num1, &num2);
    res = GCD(num1, num2);
    printf("\n GCD of %d and %d = %d", num1, num2, res);
    return 0;
}
int GCD(int x, int y)
{
    int rem;
    rem = x%y;
    if(rem==0)
        return y;
    else
        return (GCD(y, rem));
}
```

### Output

```
Enter the two numbers : 8 12
GCD of 8 and 12 = 4
```

## Finding Exponents

We can also find exponent of a number using recursion. To find x^y, the base case would be when y=0, as we know that any number raised to the power 0 is 1. Therefore, the general formula to find x^y can be given as

```
EXP (x, y) = | 1, if y = 0
             | x * EXP (x, y-1), otherwise
```

### Working

```
exp_rec(2, 4) = 2 x exp_rec(2, 3)
    exp_rec(2, 3) = 2 x exp_rec(2, 2)
        exp_rec(2, 2) = 2 x exp_rec(2, 1)
            exp_rec(2, 1) = 2 x exp_rec(2, 0)
                exp_rec(2, 0) = 1
            exp_rec(2, 1) = 2 x 1 = 2
        exp_rec(2, 2) = 2 x 2 = 4
    exp_rec(2, 3) = 2 x 4 = 8
exp_rec(2, 4) = 2 x 8 = 16
```

## PROGRAMMING EXAMPLE

### 12. Write a program to calculate exp(x,y) using recursive functions.

```c
#include <stdio.h>
int exp_rec(int, int);
int main()
{
    int num1, num2, res;
    printf("\n Enter the two numbers : ");
    scanf("%d %d", &num1, &num2);
    res = exp_rec(num1, num2);
    printf("\n RESULT = %d", res);
    return 0;
}
int exp_rec(int x, int y)
{
    if(y==0)
        return 1;
    else
        return (x * exp_rec(x, y-1));
}
```

Output
Enter the two numbers : 3 4
RESULT = 81

## The Fibonacci Series

The Fibonacci series can be given as
0 1 1 2 3 5 8 13 21 34 55 ....
That is, the third term of the series is the sum of the first and second terms. Similarly, fourth term is the sum of second and third terms, and so on. Now we will design a recursive solution to find the nth term of the Fibonacci series. The general formula to do so can be given as
As per the formula, FIB(0) = 0 and FIB(1) = 1. So we have two base cases. This is necessary because every problem is divided into two smaller problems.

```
FIB (n) = { 0, if n < 1
        1, if n = 1
        FIB (n - 1) + FIB(n - 2), otherwise }
```

## PROGRAMMING EXAMPLE

### 13. Write a program to print the Fibonacci series using recursion.

```c
#include <stdio.h>
int Fibonacci(int);
int main()
{
    int n, i = 0, res;
    printf("Enter the number of terms\n");
    scanf("%d",&n);
    printf("Fibonacci series\n");
    for(i = 0; i < n; i++ )
    {
        res = Fibonacci(i);
        printf("%d\t",res);
     return 0;
}
int Fibonacci(int n)
{
    if ( n == 0 )
        return 0;
    else if ( n == 1 )
        return 1;
    else
        return ( Fibonacci(n-1) + Fibonacci(n-2) );
}
```

Output
Enter the number of terms
Fibonacci series
0   1   1   2   3

## Types of Recursion

Recursion is a technique that breaks a problem into one or more sub-problems that are similar to the original problem. Any recursive function can be characterized based on:

- whether the function calls itself directly or indirectly (direct or indirect recursion),
- whether any operation is pending at each recursive call (tail-recursive or not), and
- the structure of the calling pattern (linear or tree-recursive).

```c
int Func ( int n )
{
    if ( n == 0)
        return n;
    else
        return ( Func ( n-1));
}
```

Figure 7.28 Direct recursion

In this section, we will read about all these types of recursions.

### Direct Recursion

A function is said to be directly recursive if it explicitly calls itself. For example, consider the code shown in Fig. 7.28. Here, the function Func() calls itself for all positive values of n, so it is said to be a directly recursive function.

```c
int Func1 ( int n )
{
    if ( n == 0)
        return n;
    else
        return Func2(n);
}
int Func2( int x )
{
    return Func1(x-1);
}
```

Figure 7.29 Indirect recursion

### Indirect Recursion

A function is said to be indirectly recursive if it contains a call to another function which ultimately calls it. Look at the functions given below. These two functions are indirectly recursive as they both call each other (Fig. 7.29).

### Tail Recursion

```c
int Fact(int n)
{
    if ( n == 1)
        return 1;
    else
        return ( n * Fact(n-1));
}
```

Figure 7.30 Non-tail recursion

A tail recursive function is said to be tail recursive if no operations are pending to be performed when the recursive function returns to its caller. When the called function returns, the returned value is immediately returned from the calling function. Tail recursive functions are highly desirable because they are much more efficient to use as the amount of information that has to be stored on the system stack is independent of the number of recursive calls.

In Fig. 7.30, the factorial function that we have written is a non-tail-recursive function, because there is a pending operation of multiplication to be performed on return from each recursive call.

```c
int Fact(int n)
{
    return Fact1(n, 1);
}
int Fact1(int n, int res)
{
    if (n == 1)
        return res;
    else
        return Fact1(n-1, n*res);
}
```

Whenever there is a pending operation to be performed, the function becomes non-tail recursive. In such a non-tail recursive function, information about each pending operation must be stored, so the amount of information directly depends on the number of calls.

However, the same factorial function can be written in a tail-recursive manner as shown Fig. 7.31. In the code, Fact1 function preserves the syntax of Fact(n). Here the recursion occurs in the Fact1 function and not in Fact function. Carefully observe that Fact1 has no pending operation to be performed on return from recursive calls. The value computed by the recursive call is simply returned without any modification.

Figure 7.31 Tail recursion

In this case, the amount of information to be stored on the system stack is constant (only the values of n and res need to be stored) and is independent of the number of recursive calls.

## Converting Recursive Functions to Tail Recursive

A non-tail recursive function can be converted into a tail-recursive function by using an auxiliary parameter as we did in case of the Factorial function. The auxiliary parameter is used to form the result. When we use such a parameter, the pending operation is incorporated into the auxiliary parameter so that the recursive call no longer has a pending operation. We generally use an auxiliary function while using the auxiliary parameter. This is done to keep the syntax clean and to hide the fact that auxiliary parameters are needed.

## Linear and Tree Recursion

```c
int Fibonacci(int num)
{
    if(num == 0)
        return 0;
    else if (num == 1)
        return 1;
    else
        return (Fibonacci(num - 1) + Fibonacci(num - 2));
}
```

Observe the series of function calls. When the function returns, the pending operations in turn calls the function

- Fibonacci(7) = Fibonacci(6) + Fibonacci(5)
- Fibonacci(6) = Fibonacci(5) + Fibonacci(4)
- Fibonacci(5) = Fibonacci(4) + Fibonacci(3)
- Fibonacci(4) = Fibonacci(3) + Fibonacci(2)
- Fibonacci(3) = Fibonacci(2) + Fibonacci(1)
- Fibonacci(2) = Fibonacci(1) + Fibonacci(0)

Now we have, Fibonacci(2) = 1 + 0 = 1
Fibonacci(3) = 1 + 1 = 2
Fibonacci(4) = 2 + 1 = 3
Fibonacci(5) = 3 + 2 = 5
Fibonacci(6) = 3 + 5 = 8
Fibonacci(7) = 5 + 8 = 13

Figure 7.32 Tree recursion

Recursive functions can also be characterized depending on the way in which the recursion grows in a linear fashion or forming a tree structure (Fig. 7.32). In simple words, a recursive function is said to be linearly recursive when the pending operation (if any) does not make another recursive call to the function. For example, observe the last line of recursive factorial function. The factorial function is linear recursive as the pending operation involves only multiplication to be performed and does not involve another recursive call to fact. On the contrary, a recursive function is said to be tree recursive (or non-linear recursive) if the pending operation makes another recursive call to the function. For example, the Fibonacci function in which the pending operations recursively call the Fibonacci function.

## Tower of Hanoi

The tower of Hanoi is one of the main applications of recursion. It says, 'if you can solve n-1 cases, then you can easily solve the nth case'.
