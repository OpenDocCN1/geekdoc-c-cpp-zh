
1. **Call by value:** Function call has number of different parameters, the value of these parameters is passed to formal parameters hence the value of actual parameters passed to formal parameters are called call by value. In this function call passes arguments by value. The called function creates a new set of variables.

**Function prototype statement is:**

```c
void call_by_value(int x)
```

**Function call statement is:**

```c
call_by_value(a);
```

**Function definition is:**

```c
void call_by_value(int x)
{
    printf("Inside call_by_value x = %d before adding 10.\n", x);
    x += 10;
    printf("Inside call_by_value x = %d after adding 10.\n", x);
}
```

## Program:

```c
#include <stdio.h>

void call_by_value(int x)
{
    printf("Inside call_by_value x = %d before adding 10.\n", x);
    x += 10;
    printf("Inside call_by_value x = %d after adding 10.\n", x);
}

void main()
{
    int a=20;
    printf("a = %d before function call_by_value.\n", a);
    call_by_value(a);
    printf("a = %d after function call_by_value.\n", a);
    getch();
}
```

## The output of the program:

```
a = 20 before function call_by_value.

Inside call_by_value x = 20 before adding 10.

Inside call_by_value x = 30 after adding 10.

a = 20 after function call_by_value.
```

In the main() we create a variable of integer type that has the value of 20. Starting value of a we are printing then function call_by_value is called and we input the variable a. This variable (a) is then copied to the function variable x. In the function we add 10 to x (and also call some print statements). Then when the next statement is called in main() function the value of variable a is printed. We can see that the value of variable a isn't changed by the call of the function call_by_value().

2. **Call by reference:** In this function, declaration and definition parameters are passed by reference. In this formal parameters of function definition become aliases to the actual arguments in the calling function.

The call by reference method of passing arguments to a function copies the address of an argument into the formal parameter. Inside the function, the address is used to access the actual argument used in the call. It means the changes made to the parameter affect the passed argument.

To pass a value by reference, argument pointers are passed to the functions just like any other value. So accordingly you need to declare the function parameters as pointer types as in the following function swap(), which exchanges the values of the two integer variables pointed to, by their arguments. The pointer variables are to be specified in function declaration and function definition.

```c
/* function definition to swap the values */
void swap(int *a, int *b)
{
    int temp;
    temp = *a;    /* save the value at address a */
    *a = *b;      /* put b into a */
    *b = temp;    /* put temp into b */
    return;
}
```

Let us now call the function swap() by passing values by reference as in the following example

```c
#include <stdio.h>
    /* function declaration */
    void swap(int *a, int *b);
    void main ()
    {
        /* local variable definition */
        int x = 10;
        int y = 20;
        printf("Before swap, value of x : %d\n", x );
        printf("Before swap, value of y : %d\n", y );
        /* calling a function to swap the values.
         * &x indicates pointer to x ie. address of variable x and
         * &y indicates pointer to y ie. address of variable y.
         */
        swap(&x, &y);
        printf("After swap, value of x : %d\n", x );
        printf("After swap, value of y : %d\n", y );
        getch();
    }
```

**Output:**

```text
Before swap, value of x :10
Before swap, value of y :20
After swap, value of x :20
After swap, value of y :10
```

## Recursive Function

**Recursion** is a process by which a function calls itself repeatedly, until some specified condition has been satisfied. Function calling itself is Recursion.

The process is used for repetitive computations in which each action is stated in terms of a previous result.

In C, Recursion is a programming technique that allows the programmer to express operations in terms of themselves.

Recursion is a process by which action calls itself repeatedly, until some specified condition has been satisfied. The process is used for repetitive computations in which each action is stated in terms of a previous result. It is similar to looping. On the other hand, recursion makes it easier to express ideas in which the result of the recursive call is necessary to complete the task.

**A simple example of recursion would be:**

```c
void recurse()
{
    recurse(); /* Function calls itself */
}
int main()
{
    recurse(); /* Sets off the recursion */
    return 0;
}
```

This program will not continue forever, however. The computer keeps function calls on a stack and once too many are called without ending, the program will crash.

## Identify the 3 parts of the recursive algorithm:

All recursive algorithm must have the following three stages:

- Base Case: if ( nargin() == 2 ) result = a + b;
- "Work toward base case": a+b becomes the first parameter
  This reduces the number of parameters to the function from 3 to 2, and 2 is the base case!
- Recursive Call: add_numbers(a+b, c);

In this algorithm, the computer “remembers” every previous state of the problem. This information is “held” by the computer on the “activation stack” (i.e., inside of each functions workspace). Every function has its own workspace PER CALL of the function.

## A quick example:

```c
void count_to_ten ( int count )
{ /* we only keep counting if we have a value less than ten*/
    if ( count < 10 )
    {
        count_to_ten( count + 1 );
    }
}
int main()
{
    count_to_ten( 0 );
}
```

This program ends when we’ve counted to ten, or more precisely, when count is no longer less than ten. This is a good base case because it means that if we have an input greater than ten, we’ll stop immediately. If we’d chosen to stop when count equaled ten, then if the function were called with the input 11, it would run out of memory before stopping.

Let's calculate the factorial of a positive integer quantity. This problem can be represented as n! = 1 x 2 x 3 x . . . x n, where n is the specified positive integer.

We can also express this problem in another way, by writing n! = n x (n - 1)! This is a recursive statement of the problem, in which the desired action (the calculation of n!) is expressed in terms of a previous result (the value of (n - 1)!, which is assumed to be known.)

Also, we know that 1! = 1 by definition. This last expression provides a stopping condition for the recursion.

## Example

```c
/* calculate the factorial of an integer quantity using recursion */
#include<stdio.h>
long int factorial(int n); /* function prototype */
void main( )
{
    int n;
    long int factorial(int n);
    /* read in the integer value */
    scanf("%d", &n);
    /* calculate and display the factorial */
    printf("n! = %ld\n", factorial(n));
    getch();
}

/* function definition */
long int factorial(int n) /* calculate the factorial */
{
    if (n <= 1)
        return( 1 );
    else
        return(n * factorial(n - 1));
}
```

The main portion of the program simply reads the integer quantity n and then calls the long-integer recursive function factorial. The function factorial calls itself recursively, with an actual argument (n - 1) that decreases in magnitude for each successive call. The recursive calls terminate when the value of the actual argument becomes equal to 1.

## Recursive Method

![](img/35ea447eca4d04af54f37bf3d3ca337d_160_0.png)

When the program is executed, the function factorial will be accessed repeatedly, once in main and (n - 1) times within itself, though the person using the program will not be aware of this. Only the final answer will be displayed; for example,

n! = 3628800

When a recursive program is executed, the recursive function calls are not executed immediately. Rather, they are placed on a *stack* until the condition that terminates the recursion is encountered. The function calls are then executed in reverse order, as they are "popped" off the stack. Thus, when evaluating a factorial recursively, the function calls will proceed in the following order.

n! = n x (n - 1)!
(n - 1)! = (n - 1) x (n - 2)!
(n - 2)! = (n - 2) x (n - 3)!
2! = 2 x 1!

The actual values will then be returned in the following reverse order.

1! = 1
2! = 2 x 1! = 2 x 1 = 2
3! = 3 x 2! = 3 x 2 = 6
4! = 4 x 3! = 4 x 6 = 24
n! = n x (n - 1)! = ...

This reversal in the order of execution is a characteristic of all functions that are executed recursively.

![](img/35ea447eca4d04af54f37bf3d3ca337d_161_0.png)
