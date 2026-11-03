```
```c
int x = 10;
int y = 20;
int p,q;
p = prod(x,y);
q = prod(p,prod(x,2));
printf("%d %d\n", p,q);
}
prod(a,b)
{
int a,b;
{
return (a*b);
}
```
```

10.50 Write a function exchange to interchange the values of two variables, say x and y. Illustrate the use of this function, in a calling function. (Hint: Assume that x and y are defined as global variables.)

10.51 Write a function space(x) that can be used to provide a space of x positions between two output numbers.

10.52 Use recursive calls to evaluate
f(x) = x - x^3/3! + x^5/5! - x^7/7! + .......

10.53 An n_order polynomial can be evaluated as follows:
P = (...((a0+a1x+a2)x+a3)x+...+an)
Write a function to evaluate the polynomial, using array variable a.

10.54 The Fibonacci numbers are defined as follows:
F1 = 1
F2 = 1
Fn = F(n-1)+F(n-2), n > 2
Write a function that will generate and print the first n Fibonacci numbers.

10.55 Write a function that will round a floating-point number to an indicated decimal places. For example the number 17.457 would yield the value 17.46 when it is rounded off to two decimal places.

10.56 Write a function prime that returns 1 if its argument is a prime number and returns zero otherwise.

10.57 Write a function that will scan a character string passed as an argument and convert all lower-case characters into their upper-case equivalents.

10.58 Write a function to raise a number to a power when both are floating point numbers.

Note: It is a good practice to use function prototypes as recommended in ANSI C. Try them if your compiler supports ANSI standards.

10.59 Explain the role of the C preprocessor.

10.60 What is a macro and how is it different from a C variable name?

10.61 When does a programmer use #include directive?

10.62 Distinguish between #ifdef and #if directives.

In #include directives, some file names are enclosed in angle brackets while others are enclosed in double quotation marks. Why?