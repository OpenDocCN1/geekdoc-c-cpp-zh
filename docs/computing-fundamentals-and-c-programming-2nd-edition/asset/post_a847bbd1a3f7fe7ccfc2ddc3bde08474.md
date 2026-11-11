
```c
TOTAL AREA = 12.005000

AREA UNDER A CURVE
Enter lower limit: 0
Enter upper limit: 3
Enter number of trapezoids: 100
TOTAL AREA = 12.000438
```

*Fig. 11.21 Computing area under a curve*

## REVIEW QUESTIONS

### Fill in the Blanks

- 1. The parameters used in a function call are called ______. (LO 11.1)
- 2. In prototype declaration, specifying ______ is optional. (LO 11.2)
- 3. A ______ aids the compiler to check the matching between the actual arguments and the formal ones. (LO 11.2)
- 4. In passing by pointers, the variables of the formal parameters must be prefixed with ______ in their declaration. (LO 11.3)
- 5. By default, ______ is the return type of a C function. (LO 11.3)
- 6. A function that calls itself is known as a ______ function. (LO 11.4)
- 7. A variable declared inside a function is called ______. (LO 11.6)
- 8. ______ refers to the region where a variable is actually available for use. (LO 11.6)
- 9. If a local variable has to retain its value between calls to the function, it must be declared as ______. (LO 11.6)
- 10. A variable declared inside a function by default assumes ______ storage class. (LO 11.6)

### True or False Statements

- 1. Any name can be used as a function name. (LO 11.1)
- 2. A function without a **return** statement is illegal. (LO 11.2)
- 3. A function prototype must always be placed outside the calling function. (LO 11.2)
- 4. The variable names used in prototype should match those used in the function definition. (LO 11.2)
- 5. The return type of a function is **int** by default. (LO 11.2)
- 6. When variable values are passed to functions, a copy of them are created in the memory. (LO 11.2)

### Levels of Difficulty

Low; Medium; High

- (c) Data type of one of the arguments in a prototype does not match with the type of the corresponding formal parameter in the header line.
- (d) The order of actual parameters in the function call is different from the order of formal parameters in a function where all the parameters are of the same type.
- (e) The type of expression used in return statement does not match with the type of the function.

- 6. Which of the following prototype declarations are invalid? Why? **LO 11.2**
    - (a) int fun (void);
    - (b) double fun (void)
    - (c) float fun (x, y, n);
    - (d) void fun (void, void);
    - (e) int fun (int a, b);
    - (f) fun (int, float, char);
    - (g) void fun (int a, int &b);

- 7. Which of the following header lines are invalid? Why? **LO 11.2**
    - (a) float average (float x, float y, float z);
    - (b) double power (double a, int n = 1)
    - (c) int product (int m, 10)
    - (d) double minimum (double x; double y);
    - (e) int mul (int x, y)
    - (f) exchange (int *a, int *b)
    - (g) void sum (int a, int b, int &c)

- 8. A function to divide two floating point numbers is as follows: **LO 11.3**

```c
divide (float x, float y)
{
    return (x / y);
}
```

What will be the value of the following “function calls”

- (a) divide (10, 2)
- (b) divide (9, 2)
- (c) divide (4.5, 1.5)
- (d) divide (2.0, 3.0)

- 9. What will be the effect on the above function calls if we change the header line as follows: **LO 11.3**
    - (a) int divide (int x, int y)
    - (b) double divide (float x, float y)

- 10. Determine the output of the following program? **LO 11.3**

```c
int prod( int m, int n);
main ( )
{
    int x = 10;
    int y = 20;
    int p, q;
    p = prod (x,y);
    q = prod (p, prod (x,z));
    printf ("%d %d\n", p,q);
}
int prod( int a, int b)
{
    return (a * b);
}
```

- 11. What will be the output of the following program?

```c
void test (int *a);
main ( )
{
    int x = 50;
    test ( &x);
    printf("%d\n", x);
}
void test (int *a)
{
    *a = *a + 50;
}
```

- 12. The function *test* is coded as follows:

```c
int test (int number)
{
    int m, n = 0;
    while (number)
    {
        m = number % 10;
        if (m % 2)
            n = n + 1;
        number = number / 10;
    }
    return (n);
}
```

What will be the values of *x* and *y* when the following statements are executed?

```c
int x = test (135);
int y = test (246);
```

- 13. Enumerate the rules that apply to a function call.
- 14. Summarize the rules for passing parameters to functions by pointers.
- 15. What are the rules that govern the passing of arrays to function?
- 16. State the problems we are likely to encounter when we pass global variables as parameters to functions.

## DEBUGGING EXERCISES

- 1. Find errors, if any, in the following function definitions: (LO 11.3)

```c
(a) void abc (int a, int b)
{
        int c;
        . . . .
        return (c);
}
(b) int abc (int a, int b)
{
        . . . .
        . . . .
}
(c) int abc (int a, int b)
{
        double c = a + b;
        return (c);
}
(d) void abc (void)
{
        . . . .
        . . . .
        return;
}
(e) int abc(void)
{
        . . . .
        . . . .
        return;
}
```

- 2. Find errors in the following function calls: (LO 11.3)

```c
(a) void xyz ( );
(b) xyz ( void );
(c) xyz ( int x, int y);
(d) xyzz ( );
(e) xyz ( ) + xyz ( );
```

## PROGRAMMING EXERCISES

- 1. Write a function **exchange** to interchange the values of two variables, say x and y. Illustrate the use of this function, in a calling function. Assume that x and y are defined as global variables. (LO 11.2)
- 2. Write a function **space(x)** that can be used to provide a space of x positions between two output numbers. Demonstrate its application. (LO 11.6)
- 3. Use recursive function calls to evaluate (LO 11.4)

  \(f(x) = x - x^3/3! + x^5/5! - x^7/7! + \cdots\)

- 4. An n-order polynomial can be evaluated as follows:

  \(P = (((...((a_0x + a_1)x + a_2)x + a_3)x + ... + a_n))\)

  Write a function to evaluate the polynomial, using an array variable. Test it using a main program.

- 5. The Fibonacci numbers are defined recursively as follows:

  \(F_1 = 1\)

  \(F_2 = 1\)

  \(F_n = F_{n-1} + F_{n-2},\ n > 2\)

  Write a function that will generate and print the first n Fibonacci numbers. Test the function for n = 5, 10, and 15.

- 6. Write a function that will round a floating-point number to an indicated decimal place. For example the number 17.457 would yield the value 17.46 when it is rounded off to two decimal places.
- 7. Write a function `prime` that returns 1 if its argument is a prime number and returns zero otherwise.
- 8. Write a function that will scan a character string passed as an argument and convert all lowercase characters into their uppercase equivalents.
- 9. Develop a top-down modular program to implement a calculator. The program should request the user to input two numbers and display one of the following as per the desire of the user:

  - (a) Sum of the numbers
  - (b) Difference of the numbers
  - (c) Product of the numbers
  - (d) Division of the numbers

  Provide separate functions for performing various tasks such as reading, calculating and displaying. Calculating module should call second level modules to perform the individual mathematical operations. The main function should have only function calls.

- 10. Develop a modular interactive program using functions that reads the values of three sides of a triangle and displays either its area or its perimeter as per the request of the user. Given the three sides a, b and c.

  \(\text{Perimeter} = a + b + c\)

  \(\text{Area} = \sqrt{s(s-a)(s-b)(s-c)}\)

  where

  \(s = (a+b+c)/2\)

- 11. Write a function that can be called to find the largest element of an m by n matrix.
- 12. Write a function that can be called to compute the product of two matrices of size m by n and n by m. The main function provides the values for m and n and two matrices.
- 13. Design and code an interactive modular program that will use functions to read a matrix of m by n size, compute column averages and row averages, and then print the entire matrix with averages shown in respective rows and columns.
- 14. Develop a top-down modular program that will perform the following tasks:

  - (a) Read two integer arrays with unsorted elements.
  - (b) Sort them in ascending order
