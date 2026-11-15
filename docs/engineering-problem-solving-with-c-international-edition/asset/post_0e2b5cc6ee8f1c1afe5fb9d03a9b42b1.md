
## Factorial Computation

A simple example of recursion can be shown using the **factorial** computation. Recall that k! (read as k factorial) is defined as

```
k! = (k)(k - 1)(k - 2) ... (3)(2)(1),
```

where k is a nonnegative integer, and where 0! = 1. Thus,

```
5! = 5 * 4 * 3 * 2 * 1 = 120,
```

We could also compute 5! using the following steps:

```
5! = 5 * 4!
4! = 4 * 3!
3! = 3 * 2!
2! = 2 * 1!
1! = 1 * 0!
0! = 1.
```

Thus, we have defined a factorial in terms of a product that involves smaller factorials. The smaller factorial is continually redefined until we reach 0!. We substitute the value of 0! in the last equation, and then begin going back up the list of equations, substituting values for the factorials:

```
1! = 1 * 1
2! = 2 * 1! = 2
3! = 3 * 2! = 6
4! = 4 * 3! = 24
5! = 5 * 4! = 120.
```

We have now developed a recursive algorithm for computing a factorial.

We present a program with two functions to compute a factorial. The first function is a nonrecursive (iterative) function, and the second is a recursive function. A factorial value becomes large quickly, so we use long integers for the factorial value. Note that both functions are referenced similarly in the main function:

```
/*-------------------------------------------------*/
/* Program chapter4_10                             */
/*                                                 */
/* This program compares a recursive function and  */
/* a nonrecursive function for computing factorials. */
/*                                                 */
#include <stdio.h>
int main(void)
{
   /* Declare variables and function prototypes. */
   int n;
   long factorial(int k);
   long factorial_r(int k);
   /* Get user input. */
   printf("Enter positive integer: \n");
   scanf("%i", &n);
   /* Compute and print factorials. */
   printf("Nonrecursive: %i! = %li \n",n,factorial(n));
   printf("Recursive: %i! = %li \n",n,factorial_r(n));
   /* Exit program. */
   return 0;
}
```

```
/*--------------------------------------------------------------*/
/* This function computes a factorial with a loop. */
long factorial(int k)
{
/* Declare variables. */
int j;
long term;
/* Compute factorial with multiplication. */
term = 1;
for (j=2; j<=k; j++)
term *= j;
/* Return factorial value. */
return term;
}
```

```
/*--------------------------------------------------------------*/
/* This function computes a factorial recursively. */
long factorial_r(int k)
{
/* Use recursive reference until k=0. */
if (k == 0)
return 1;
else
return k*factorial_r(k-1);
}
```

The condition k == 0 keeps the recursive routine from becoming an infinite loop; this routine calls itself recursively with an argument that is continually being decremented by 1, until the argument reaches zero.

For large values of k, the value of k! can exceed even long integers. In these cases, the computations should be done using double or long double values. An interesting approximation to k! is also discussed in the end-of-chapter problems.

## Fibonacci Sequence

A **Fibonacci sequence** is a sequence of numbers \(\{f_0, f_1, f_2, f_3, \dots\}\) in which the first two values (\(f_0\) and \(f_1\)) are equal to 1, and each succeeding number is the sum of the previous two numbers. Thus, the first few values of the Fibonacci sequence are

1 1 2 3 5 8 13 21 34 ...

This sequence was first described in the year 1202, and it has applications that range from biology to electrical engineering. For example, Fibonacci sequences are often used in studies of rabbit population growth.

A function to compute the \(k\)th value in the Fibonacci sequence is a good candidate for a recursive function because each new value in the sequence is computed from the two previous values. The following functions implement both nonrecursive and recursive algorithms for computing a Fibonacci number:

```
/*
-----------------------------------------------
Program chapter4_11
-----------------------------------------------
*/
/*
* This program compares a recursive function and a
* nonrecursive function for computing Fibonacci numbers.
*/
#include <stdio.h>
int main(void)
{
   /* Declare variables and function prototypes. */
   int n;
   int fibonacci(int k);
   int fibonacci_r(int k);

   /* Get user input. */
   printf("Enter positive integer: \n");
   scanf("%i",&n);

   /* Compute and print factorials. */
   printf("Nonrecursive: Fibonacci number = %li \n",
          fibonacci(n));
   printf("Recursive: Fibonacci number = %li \n",
          fibonacci_r(n));

   /* Exit program. */
   return 0;
}
/*
-----------------------------------------------
* This function computes the kth Fibonacci
* number using a nonrecursive algorithm.
*/
int fibonacci(int k)
{
   /* Declare variables. */
   int term, prev1, prev2, n;
   /* Compute kth Fibonacci number with a loop. */
   term = 1;
   if (k > 1)
   {
       prev1 = prev2 = 1;
       for (n=2; n<=k; n++)
       {
           term = prev1 + prev2;
           prev2 = prev1;
           prev1 = term;
       }
   }
   /* Return kth Fibonacci number. */
   return term;
}
```

```
/* This function computes the kth Fibonacci
* number using a recursive algorithm.
*/
int fibonacci_r(int k)
{
    /* Declare variables. */
    int term;
    /* Compute kth Fibonacci number recursively until k=1. */
    term = 1;
    if (k > 1)
        term = fibonacci_r(k-1) + fibonacci_r(k-2);
    /* Return kth Fibonacci number. */
    return term;
}
```

In the recursive function, the condition k > 1 keeps the function from going into an infinite loop.

## MODIFY!

- 1. Use the program chapter4_12 to compute values of 1!, 2!, and so on, until you reach the limits for long integers. What kind of error message occurred when the value of k! exceeded the limits on your system?
- 2. Modify Chapter4_12 so that it uses double values instead of integers to compute factorials. Explain why the number of digits of precision determines the maximum value of k! that can be correctly computed using double values. What is the maximum value of k! that can be computed using double values on your system?

Most programs in C benefit from using both library and programmer-defined functions. Functions allow us to reuse software and to employ abstraction in our solution and, hence, reduce development time and increase the quality of the software. Numerous examples were developed to illustrate using programmer-defined functions to solve problems, including examples of macros and recursive functions. Specific applications were presented to illustrate generating random numbers (integers or floating-point values) and to implement the incremental search technique for identifying real roots of polynomials.

## KEY TERMS

- abstraction local variable
- actual parameter macro
- automatic class modularity
- call-by-reference module
- call-by-value module chart
- coercion of arguments programmer-defined function
- computer simulation pseudorandom
- driver program random number
- external class random number seed
- factorial recursion
- Fibonacci sequence register class
- formal parameter reusability
- function root
- function prototype scope
- global variable static class
- incremental search storage class
- invoke structure chart
- library function

## C STATEMENT SUMMARY

```
Function definition:
return_type function_name(parameter types)
{
    declarations;
    statements;
}

Return statement:
return;
return (a + b)/2;

Function prototype:
double sinc(double x);
double sinc(double);
void check_roots(double left,double right,double a0,
    double a1,double a2,double a3)

Macro:
#define degrees_C(x) (((x) - 32)*(5.0/9.0))
```

## NOTES

- 1. A program with several modules is easier to read and understand than one long main function.
- 2. Select the name of the function to indicate the purpose of the function.
- 3. Use a special line, such as a line of dashes, to separate programmer-defined functions from the main function and other programmer-defined functions.
- 4. Use a consistent order for functions. For instance, place the main function first, followed by additional functions in the order in which they are referenced.
- 5. Use parameter identifiers in prototype statements to help document the order and definition of the parameters.
- 6. List the function prototypes on separate lines so that they are easy to identify.
- 7. Use the parameter list instead of external variables to transmit information to a function.

## DEBUGGING NOTES

- 1. If you are having difficulty understanding the error messages from a compiler, try running the program on another compiler to obtain different error messages.
- 2. When debugging a long program, add comment indicators (/* and */) around some sections of the code so that you can focus on other parts of the program.
- 3. Test a complicated function by itself using a driver program.
- 4. Make sure that the value returned from a function matches the function return type. If necessary, use the cast operator to convert a value to the proper type.
- 5. Functions can be defined before or after the main function, but not within it.
- 6. Always use function prototype statements to avoid errors in parameter passing.
- 7. Use print statements to generate memory snapshots of the actual parameters before a function is referenced, and of the formal parameters at the beginning of the function.
- 8. Carefully match the type, order, and number of actual parameters with the formal parameters of a function.
- 9. In a macro definition, each argument and the entire body should be enclosed in its own set of parentheses.
- 10. System-dependent limitations can occasionally cause problems with recursive solutions to a problem.

## PROBLEMS

### SHORT-ANSWER PROBLEMS

### True-False Problems

Indicate whether the following statements are true (T) or false (F):

- 1. The body of a function is contained in braces. T F
- 2. The parameter list (or argument list) contains all variables used by the function. T F
- 3. In a call-by-value reference, a function cannot change the value of an actual parameter. T F
- 4. A static variable is declared inside a function, but it retains its value from one reference call to another. T F
