```
p = prod (x,y);
q = prod (p, prod (x,z));
printf ("%d %d\n", p,q);
}
int prod( int a, int b)
{
    return (a * b);
}
```

```
int m, n = 0;
while (number)
{
    m = number % 10;
    if (m % 2)
    {
        n = n + 1;
        number = number /10;
    }
}
return (n);
```

# 5.15 What will be the output of the following program?

```
void test (int *a);
main ()
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

# 5.16 The function test is coded as follows:

int test (int number)
What will be the values of x and y when the following statements are executed?
int x = test (135);
int y = test (246);

+   5.17 Enumerate the rules that apply to a function call.
+   5.18 Summarize the rules for passing parameters to functions by pointers.
+   5.19 What are the rules that govern the passing of arrays to function?
+   5.20 State the problems we are likely to encounter when we pass global variables as parameters to functions.

# Programming Exercises

+   5.1 Write a function exchange to interchange the values of two variables, say x and y. Illustrate the use of this function, in a calling function. Assume that x and y are defined as global variables.
+   5.2 Write a function space(x) that can be used to provide a space of x positions between two output numbers. Demonstrate its application.
+   5.3 Use recursive function calls to evaluate f(x) = x^3/3! + x^5/5! - x^7/7! + ....
+   5.4 An n_order polynomial can be evaluated as follows: P = (...(((a0 x + a1) x + a2) x + a3) x + ... + an) Write a function to evaluate the polynomial, using an array variable. Test it using a main program.
+   5.5 The Fibonacci numbers are defined recursively as follows: F1 = 1 F2 = 1 F_n = F_{n-1} + F_{n-2}, n > 2

+   Write a function that will generate and print the first n Fibonacci numbers. Test the function for n = 5, 10, and 15.
+   5.6 Write a function that will round a floating-point number to an indicated decimal place. For example the number 17.457 would yield the value 17.46 when it is rounded off to two decimal places.
+   5.7 Write a function prime that returns 1 if its argument is a prime number and returns zero otherwise.
+   5.8 Write a function that will scan a character string passed as an argument and convert all lowercase characters into their uppercase equivalents.
+   5.9 Develop a top_down modular program to implement a calculator. The program should request the user to input two numbers and display one of the following as per the desire of the user: (a) Sum of the numbers