
## Point out the errors, if any, in the following programs:

### 1.

```c
main()
{
    int a = 3, b = 4, c, d, k;
    c = summult(a, b);
    d = summult(a, b);
    printf("\n%d", c, d);
}
summult(int x, int y)
{
    int a1, b1;
    a1 = x + y;
    b1 = x * y;
    return (a1, b1);
}
```

Output: Error. More than one value can't be returned by a function.

### 2.

```c
main()
{
    int x;
    x = message();
}
message()
{
    printf("\n your computer can be affected by Viruses:");
    return;
}
```

Output: No Error.

### 7.

```c
main()
{
    message();
    message();
}
message()
{
    printf("Whole world is waiting for you:");
}
```

Output: Error. Function definition must not be present immediately after the function definition.

### 8.

```c
main()
{
    matrix()
    {
        printf("Welcome in the world of computer:");
    }
}
```

Output: Error. One function can't be defined into the body of another function.

### 9.

```c
main()
{
```

Output: Because here no explicit return type is prefixed in function definition so default return type is int and here return statement is also exist in function definition so it will return a garbage integer value. But if there will be void type in function definition then error is encountered.

### 3.

```c
main()
{
    float a = 185.5;
    char ch = 'C';
    display(a, ch);
}

display(a, ch)
{
    printf("\n%f %c", a, ch);
}
```

Output: Error.
Formal arguments don't have any data type in function definition.

### 4.

```c
main()
{
    int a = 35, b;
    b = check(a);
    printf("\n %d", b);
}
check(m)
{
    int m;
    if(m > 40)
        return(1);
    else
        return(0);
}
```

```c
Matrix(computer());
}
void computer()
{
    printf("Beginning with C:");
}
```

### 9. main()

```c
main()
{
    int i = 135, a = 135, k;
    k = demo(i, a);
    printf("\n %d", k);
}
demo(int j, int b)
int c;
{
    c = j + b;
    return (c);
}
```

Output: Error. The declaration int c should be inside the body of demo().

### 10. main()

```c
main()
{
    int p = 23, f = 24;
    out(&p, &f);
    printf("\n%d", p, f);
}
out (int q, int g)
{
    q = q + q;
    g = g + g;
}
```

Output: Error. The variable q and g in function definition should be declared as integer pointer.

Output: Error. The variable m must be declared before the braces. The formal argument can be declared by the following two ways:

```c
(a) Check(int m)
{
}
(b) check()
int m;
{
}
```

### 5. main()

```c
main()
{
    display();
}
void display()
{
    printf("Matrix");
}
```

Output: Error of redeclaration because display() is called before it is defined. In such cases the compiler assumes that the function display() is declared as int display (); that is, an undeclared function is assumed to return an int and accept an unspecified number of arguments. Then when we define the function the compiler finds that it is returning void hence the compiler reports the discrepancy.

### 6. main()

```c
main()
{
    int a = 1;
    while(a <= 5)
```

### 11. main()

```c
main()
{
    int i = 35, *z;
    z = fun(&i);
    printf("\n%d", z);
}
fun( int *m)
{
    return(m + 2);
}
```

Output: Unpredictable Output.
Here in the above program the address of i(&i) suppose 2005 is passed to m so m contains the address of i and returns m+2 is equal to 2007. so this function return 2007 to the main() that will store in z and z gets printed through printf(). Here address is assumed by the compiler so we can't say what will be the output but there will be printed an int value.

### 13. main()

```c
main()
{
    int a, b;
    a = sumdig(123);
    b = sumdig(123);
    printf("%d %d", a, b);
}
sumdig(int n)
{
    static int s = 0;
    int d;
    if(n != 0)
    {
        d = n % 10;
        n = (n - d) / 10;
        s = s + d;
        sumdig(n);
    }
    else
        return(s);
}
```

Output: 6 12

```c
{
    printf("%d", a);
    if (a > 2)
        goto abc;
}
fun()
{
abc:
    printf("Author Harry");
}
```

Output: goto cannot take control to a different function.

```c
main()
{
    int a = 10;
    void f();
    a = f();
    printf("%d", a);
}
void f()
{
    printf("Hello");
}
```

Output: The function has been declared as void but still the program is trying to collect the value returned by f() in variable a.

### 14.

```c
f(int a, int b)
{
    int a;
    a = 20;
    return a;
}
```

Output: Error. The variable a is redeclared.

### 15.

```c
main()
{
    int b = 10;
    b = f(20);
    printf("%d", b);
}
int f(int a)
{
    a > 20?
    return(10):return(20);
}
```

Output: return statement cannot be used as shown with the conditional operators. Instead the following can be used:
`return(a > 20 ? 10 : 20);`

## State whether the following statements are True or False:

- 1. The variables commonly used in C functions are available to all functions in a program.
- 2. To return the control back to the calling function we must use the keyword return. The same variable names can be used in different functions without any conflict.
- 3. Every called function must contain a return statement.
- 4. A function may contain more than one return statement.
- 5. Each return statement in a function may return a different value.
- 6. A function can still be useful even if you don't pass any arguments to it and the function doesn't return any value back.
- 7. Same names can be used for different functions without any conflict.
- 8. A function may be called more than once from any other function.
- 9. It is necessary for a function to return some value.
- 10. A function can have several declarations but only one definition.
- 11. A function cannot be defined inside another function.
- 12. Will the following function work:

```c
main()
{
    f1(int a, int b);
    {
        return(f2(20));
    }
    f2 (int a)
    {
        return(a * a);
    }
}
```

- 13. In a function two return statements should never occur.
- 14. In a function two return statements should never occur successively.
- 15. In C all functions except main() can be called recursively.
- 16. Usually recursion works slower than loops.
- 17. Too many recursive calls may result in stack overflow.

## Answers:

|  |  |  |  |
|---|---|---|---|
| 1. False | 2. False | 3. True | 4. False |
| 5. True | 6. True | 7. True | 8. False |
| 9. False | 10. True | 11. True | 12. True |
| 13. False | 14. True | 15. False |  |
| 16. True | 17. True |  |  |

## Answer the following:

1. When we mention the prototype of a function we are defining or declaring the function?

Output: declaring

2. There is a mistake in the following code, add a statement to remove it.

```c
main()
{
    int a;
    a = f(10, 3, 14);
    printf("%d", a);
}
f(int aa, float bb)
{
    return((float)aa + bb);
}
```

Output:
The declaration of the function f is missing add the following above main()

```c
float f(int, float);
```

3. What are the two notations of defining functions commonly known as:

```c
int f( int a, float b)
{
    /*some code*/
}
int f(a, b)
int a;
float b;
{
    /*some code*/
}
```

Output:
The first one is known as ANSI notation and the second is known as Kernighan and Ritchie or simply K&R notation.

## Lab Exercise —

- 1. Write a function which takes two integers as arguments and returns their sum. WAP to test this function.
- 2. Write a function which takes two integers as arguments and returns their average in float. WAP to test this function.
- 3. WAP that uses a function that converts a lowercase character to its uppercase.
- 4. WAP that uses a function that calculates factorial of a given number.
- 5. WAP that uses a function power that calculates the power of a given number.
- 6. WAP that uses a function that finds the largest of three integer quantities.
- 7. WAP that receives any year from the keyboard and uses a function to determine whether the year is a leap year or not.
- 8. WAP that uses a function which receives a float and an int from main(), finds the product of these two and returns the product which is printed through main().
- 9. WAP that uses a function to calculate the sum of n odd integers.
- 10. WAP that uses a function to calculate the sum of n even integers starting from a given even integer.
- 11. WAP that uses a function to determine whether a given positive integer is a prime number or not.
- 12. WAP that uses a function to determine whether a given positive integer is a fibonacci number or not.
- 13. WAP that uses a function that finds the length of the largest monotonically increasing subsequence in a sequence of real numbers.
- 14. WAP that uses a function for finding the absolute value of the integer parameter passed to it (do not use any library function).
- 15. WAP that uses a function that takes two arguments: a character and an integer and prints the character given number of times. if however the integer is missing the function prints the character twice.
- 16. WAP that uses a function to sum n natural numbers starting from a given number.
- 17. WAP that uses a function that takes a character argument and prints it number of times equal to number of times that function has been called to the input.
- 18. WAP that uses a function which takes a real number as its argument and returns the sum of digits(complete including fraction parts) of this number.
- 19. WAP that uses a function that checks whether the given number is divisible by 11 or not by using the algorithm which states that a number is divisible by 11 if and only if the difference of the sums of digits at odd positions and even positions is either zero or divisible by 11.
- 20. WAP that uses a function isdigit which should return a non-zero if the given number is a digit and 0 if not.
- 21. WAP that uses a function isalpha which should return a non-zero if the
