
situations, we may repeat the program statements wherever they are needed. Another approach is to design a function that can be called and used whenever required. This saves both time and space.

This sub-sectioning approach clearly results in a number of advantages.

- 1. It facilitates top-down modular programming as shown in Fig. 10.1. In this programming style, the high level logic of the overall problem is solved first while the details of each lower-level function are addressed later.
- 2. The length of a source program can be reduced by using functions at appropriate places. This factor is particularly critical with microcomputers where memory space is limited.
- 3. As mentioned earlier, it is easy to locate and isolate a faulty function for further investigations.
- 4. A function may be used by many other programs. This means that a C programmer can build on what others have already done, instead of starting over, from scratch.

![](img/65953ea584e494f3d396b2252cb5ea53_255_0.png)

Fig. 10.1 Top-down modular programming, using functions

## 10.3 A MULTI-FUNCTION PROGRAM

A function is a self-contained block of code that performs a particular task. Once a function has been designed and packed, it can be treated as a 'black box' that takes some data from the main program and returns a value. The inner details of operation are invisible to the rest of the program. All that the program knows about a function is: What goes in and what comes out. Every C program can be designed using a collection of these black boxes.

Consider a set of statements as shown below:

```c
println()
{
    int i;
    for (i=1; i<40; i++)
        printf("-");
    printf("\n");
}
```

The above set of statements defines a function called println which could print a line of 39-character length. This function can be used in a program as follows:

```c
main()
{
    println();
    printf("This illustrates the use of C functions \n");
    println();
}

println()
{
    int i;
    for(i=1; i<40; i++)
        printf("-");
    printf("\n");
}
```

This program will print the following output:

This illustrates the use of C functions

The above program contains two user-defined functions:

- `main()`
- `println()`

As we know, the program execution always begins with the main function. During execution of the main, the first statement encountered is `println();`, which indicates that the function println is to be executed. At this point, the program control is transferred to the function println. After executing the println function which outputs a line of 39 character length, the control is transferred back to the main. Now, the execution continues at the point where the function call was executed. After executing the printf statement, the control is again transferred to the println function for printing the line once more.

The main function calls the user-defined println function two times and the library function printf once. We may notice that the println function itself calls the library function printf repeatedly.

Any function can call any other function. In fact, it can call itself. A 'called function' can also call another function. A function can be called more than once. In fact, this is one of the main features of using functions. Figure 10.2 illustrates the flow of control in a multi-function program.

Except the starting point, there are no other predetermined relationships, rules of precedence, or hierarchies among the functions that make up a complete program. The functions can be placed in any order. A called function can be placed either before or after the calling function. However, it is the usual practice to put all the called functions at the end.

### Important Note

During the last few years of applications of C, the way the functions have been defined and declared has undergone changes. The major change is the way the function arguments are declared. There are now two established methods of declaring the parameters. The older method (known as "classic" method) declares function arguments separately after the definition of function name (known as function header). The newer method (known as "modern" or ANSI method) combines the function definition and arguments declaration in one line. Luckily the modern compilers support both the methods. That is, we can write a function using either of them and execute it successfully.

Since a large number of existing programs and functions have been written using the older method, we should be familiar with this approach. The sections that follow (Secs 10.4 through 10.15) will discuss and use the classic form of function definitions and declarations. The modern ANSI method is discussed in Sec. 10.16.

![](img/65953ea584e494f3d396b2252cb5ea53_257_0.png)

Fig. 10.2 Flow of control in a multi-function program

## 10.4 THE FORM OF C FUNCTIONS

All functions have the form:

```c
function-name(argument list)
argument declaration;
{
    local variable declarations:
    executable statement1;
    executable statement2;
    --------
    --------
    return(expression);
}
```

A function may or may not send back any value to the calling function. If it does, it is done through the **return** statement. While it is possible to pass to the called function any number of values, the called function can only return *one value* per call, at the most.

The **return** statement can take one of the following forms:

```c
return;
```

或

```c
return(expression);
```

The first, the 'plain' **return** does not return any value; it acts much as the closing brace of the function. When a **return** is encountered, the control is immediately passed back to the calling function. An example of the use of a simple **return** is as follows:

```c
if(error)
    return;
```

The second form of **return** with an expression returns the value of the expression. For example, the function

```c
mul(x,y)
int x,y;
{
    int p;
    p = x*y;
    return(p);
}
```

returns the value of **p** which is the product of the values of **x** and **y**. The last two statements can be combined into one statement as follows:

```c
return (x*y);
```

A function may have more than one **return** statement. This situation arises when the value returned is based on certain conditions. For example:

```c
if(x <= 0)
    return(0);
else
    return(1);
```

What type of data does a function return? All functions by default return **int** type data. But what happens if a function must return some other type? We can force a function to return a particular type of data by using a *type specifier* in the function header. Example:

```c
double product(x,y)
float sqr_root(p)
```

When a value is returned, it is automatically cast to the function's type. In functions that do computations using **double**, yet return **int**, the returned value will be truncated to an integer.

## 10.6 CALLING A FUNCTION

A function can be called by simply using the function name in a statement. Example:

```c
main()
{
    int p;
    p = mul(10,5);
    printf("%d\n", p);
}
```

When the compiler encounters a function call, the control is transferred to the function mul(x,y). This function is then executed line by line as described and a value is returned when a return statement is encountered. This value is assigned to p.

A function which returns a value can be used in expressions like any other variable. Each of the following statements is valid:

```c
printf("%d\n", mul(p,q));
y = mul(p,q) / (p+q);
if (mul(m,n)>total) printf("large");
```

However, a function cannot be used on the left side of an assignment statement. For instance,

```c
mul(a,b) = 15;
```

is invalid.

A function that does not return any value may not be used in expressions; but can be called to perform certain tasks specified in the function. The function println() discussed in Sec. 10.3 belongs to this category. Such functions may be called by simply stating their names as independent statements.

Example:

```c
main()
{
    println();
}
```

Note the presence of a semicolon at the end.

## 10.7 CATEGORY OF FUNCTIONS

A function, depending on whether arguments are present or not and whether a value is returned or not, may belong to one of the following categories:

- Category 1: Functions with no arguments and no return values
- Category 2: Functions with arguments and no return values
- Category 3: Functions with arguments and return values.

In the sections to follow, we shall discuss these categories with examples.

## 10.8 NO ARGUMENTS AND NO RETURN VALUES

When a function has no arguments, it does not receive any data from the calling function. Similarly, when it does not return a value, the calling function does not receive any data from the called function. In effect, there is no data transfer between the calling function and the called function. This is depicted in Fig. 10.3. The dotted lines indicate that there is only a transfer of control but not data.
