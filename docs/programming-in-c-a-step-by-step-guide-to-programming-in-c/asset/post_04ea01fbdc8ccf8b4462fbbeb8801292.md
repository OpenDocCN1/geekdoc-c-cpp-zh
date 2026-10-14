
We should say a little more about the mechanism by which an argument is passed down from a caller into a function. Formally, C is *call by value*, which means that a function receives *copies* of the values of its arguments. We can illustrate this with an example. Suppose, in our implementation of **multbyfour**, we had gotten rid of the unnecessary **retval** variable like this:

```
int multbyfour(int x)
{
x = x * 4;
return x;
}
```

We might wonder, if we wrote it this way, what would happen to the value of the variable i when we called
j = multbyfour(i);

When our implementation of **multbyfour** changes the value of x, does that change the value of i up in the caller? The answer is no. x receives a copy of i's value, so when we change x we don't change i.

However, there is an exception to this rule. When the argument you pass to a function is not a single variable, but is rather an array, the function does *not* receive a copy of the array, and it therefore *can* modify the array in the caller. The reason is that it might be too expensive to copy the entire array, and furthermore, it can be useful for the function to write into the caller's array, as a way of handing back more data than would fit in the function's single return value. We will discuss more about passing arrays as arguments to a function later.

There may be several different calls to the same function from various places within a program. The actual arguments may differ from one function call to another. Within each function call, however, the actual arguments must correspond to the formal arguments in the function definition; i.e. the actual arguments must match in number and type with the corresponding formal arguments.

## Program 5.1: A program to find the largest of three integers

```
#include<stdio.h>
main()
{
int x, y, z, w;
/* read the integers */
int max(int, int);
printf("\nx= ");
scanf("%d", &x);
printf("\ny= ");
scanf("%d", &y);
printf("\nz= ");
scanf("%d", &z);
/* Calculate and display the maximum value */
w= max(x,y);
printf("\n\nmaximum=%d\n", max(z,w));
}
int max(int a, int b)
{
int c;
c=(a>=b)?a:b;
return c;
}
```

Please execute this program and observe the result.

Function calls can span several levels within a program; function A can call function B, which can call function C and so on.

## Program 5.2: Program to check whether a given integer is a perfect square or not.

```
#include<stdio.h>
main()
{
int psquare(int);
int num;
printf(" Enter the number:");
scanf("%d", &num);

if(psquare(num)) /* main() calls the function psquare() */
{
    printf("%d is a perfect square\n", num);
}
else
    printf("%d is not a perfect square\n", num);
}

int psquare(int x)
{
int positive(int);
float sqr;
if(positive(x)) /* psquare() in turn calls the function positive() */
{
    sqr = sqrt(x);
    if(sqr - (int)sqr == 0)
        return 1;
    else
        return 0;
}
}

int positive(int m)
{
    if(m>0)
        return 1;
    else return 0;
}
```

Execute the above program and observe the result.

In the above program the main function calls the function psquare() and it in turn calls the function positive() to check whether the number to be checked for perfect square is a positive or not before checking.

The return statement can be absent altogether from a function definition, though this is generally regarded as a poor programming practice. If a function reaches end of the block without encountering a return statement, control simply reverts back to the calling portion of the program without returning any information. Using an empty return statement(without the accompanying expressions) is recommended.

### Example 5.2: The following function accepts two integers and determines the larger one, which is then written out. The function doesn’t return any information to the calling program.

```
void max(int x, int y)
{
    int m;
    m = (x >= y) ? x : y;
    printf("The larger integer is = %d\n", m);
    return;
}
```

## Self Assessment Questions

- 1. The function main() is optional in a C program. (True/False)
- 2. If the function is defined elsewhere (not in the same program where it is called), the function prototype must be preceded by the keyword __________.
- 3. The arguments that appear in function definition are called ________ arguments whereas the arguments that appear when the function is called are the ________ arguments.
- 4. The return data type, function name and the list of formal parameters enclosed in brackets are separated by __________.

## 5.3 Function Prototypes

In modern C programming, it is considered good practice to use prototype declarations for all functions that you call.

As we mentioned, these prototypes help to ensure that the compiler can generate correct code for calling the functions, as well as allowing the compiler to catch certain mistakes you might make.

In general terms, a function prototype can be written as

```
data-type name(type1, type2, ..., type n)
```

Examples:

int sample(int, int) or int sample(int a, int b);

float fun(int, float) or float fun( int a, float b);

void demo(void); Here void indicates function neither return any value to the caller nor it has any arguments.

If you write the function definition after the definition of its caller function, then the prototype is required in the caller, but the prototype is optional if you write the definition of the function before the definition of the caller function. But it is good programming practice to include the function prototype wherever it is defined.

If prototypes are a good idea, and if we're going to get in the habit of writing function prototype declarations for functions we call that we've written (such as multbyfour), what happens for library functions such as printf? Where are their prototypes? The answer is in that boilerplate line

```
#include <stdio.h>
```

we've been including at the top of all of our programs. stdio.h is conceptually a file full of external declarations and other information pertaining to the “Standard I/O” library functions, including printf. The #include directive arranges all of the declarations within stdio.h that are considered by the compiler, rather as if we'd typed them all in ourselves. Somewhere within these declarations is an external function prototype declaration for printf, which satisfies the rule that there should be a prototype for each function we call. (For other standard library functions we call, there will be other “header files" to include.) Finally, one more thing about external function prototype declarations: we've said that the distinction between external declarations and defining instances of normal variables hinges on the presence or absence of the keyword extern. The situation is a little bit different for functions. The “defining instance" of a function is the function, including its body (that is, the brace-enclosed list of declarations and statements implementing the function). An external declaration of a function, even without the keyword extern, looks nothing like a function declaration. Therefore, the keyword extern is optional in function prototype declarations. If you wish, you can write `int multbyfour(int);` and this is just like an external function prototype declaration as `extern int multbyfour(int);` (In the first form, without the extern, as soon as the compiler sees the semicolon, it knows it's not going to see a function body, so the declaration can't be a definition.) You may want to stay in the habit of using extern in all external declarations, including function declarations, since “extern = external declaration" is an easier rule to remember.

## Program 5.3: Program to illustrate that the function prototype is optional in the caller function. The program is to convert a character from lowercase to uppercase.

```
#include<stdio.h>
char lower_to_upper(char ch) /* Function definition precedes main() */
{
char c;
c=(ch>='a' && ch<='z') ? ('A'+ch-'a'):ch;
return c;
}

main()
{
char lower, upper;
```
