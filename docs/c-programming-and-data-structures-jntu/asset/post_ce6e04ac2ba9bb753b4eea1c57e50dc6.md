
compiled separately and linked later to form an executable object code. This approach is very useful because any change in one file does not affect other files thus eliminating the need for recompilation of the entire program.

Multiple source files can share a variable provided it is declared as an external variable appropriately. Variables that are shared by two or more files are global variables and therefore we must declare them accordingly in one file and then explicitly define them with extern in other files. Figure 10.15 illustrates the use of extern declarations in a multifile program.

The function main in file1 can reference the variable m that is declared as global in file2. Remember, function1 cannot access the variable m. If, however, the extern int m; statement is placed before main, then both the functions could refer to m. This can also be achieved by using extern int m; statement inside each function in file1.

The extern specifier tells the compiler that the following variable types and names have already been declared elsewhere and no need to create storage space for them. It is the responsibility of the linker to resolve the reference problem. It is important to note that a multifile global variable should be declared without extern in one (and only one) of the files. The extern declaration is done in places where secondary references are made. If we declare a variable as global in two different files used by a single program, then the linker will have a conflict as to which variable to use and, therefore, issues a warning.

## file1.c

```
main()
{
    extern int m;
    int i;
    ....
    ....
}
function1()
{
    int j;
    ....
    ....
}
```

## file2.c

```
int m /* global variable */
function2()
{
    int i;
    ....
    ....
}
function3()
{
    int count;
    ....
    ....
}
```

Fig. 10.15 Use of extern in a multifile program

The multifile program shown in Fig. 10.15 may be modified as shown in Fig. 10.16.

When a function is defined in one file and accessed in another, the later file must include a function declaration. The declaration identifies the function as an external function whose definition appears elsewhere. We usually place such declarations at the beginning of the file, before all functions. Although all functions are assumed to be external, it would be a good practice to explicitly declare such functions with the storage class extern.

## Static Variables

As the name suggests, the value of static variables persists until the end of the program. A variable can be declared static using the keyword static like:

## file1.c

```
int m; /* global variable */
main()
{
    int i;
    ....
    ....
}
function1()
{
    int j;
    ....
    ....
}
```

## file2.c

```
extern int m;
function2()
{
    int i;
    ....
    ....
}
function3()
{
    int count;
    ....
    ....
}
```

Fig. 10.16 Another version of a multifile program

```
static int x;
static float y;
```

A static variable may be either an internal type or an external type, depending on the place of declaration.

Internal static variables are those which are declared inside a function. The scope of internal static variables extends up to the end of the function in which they are defined. Therefore, internal static variables are similar to auto variables, except that they remain in existence (alive) throughout the remainder of the program. Therefore, internal static variables can be used to retain values between function calls. For example, it can be used to count the number of calls made to a function.

## Example 10.9

Write a program to illustrate the properties of a static variable.

The program in Fig. 10.17 explains the behaviour of a static variable.

```
Program
/*---------------------------------------------------------------*/
/* ILLUSTRATION OF STATIC VARIABLE */
/*---------------------------------------------------------------*/
main()
{
    int i;
    for(i=1; i<=3; i++)
        stat();
}
stat()
{
    static int x = 0;
    x = x + 1;
    printf("x = %d\n", x);
}
```

Output
x = 1
x = 2
x = 3

## Fig. 10.17 Illustration of static variable

A static variable is initialized only once, when the program is compiled. It is never initialized again. During the first call to stat, x is incremented to 1. Because x is static, this value persists and therefore, the next call adds another 1 to x giving it a value of 2. The value of x becomes three when the third call is made.

```
x = 1
x = 1
x = 1
```

This is because each time stat is called, the auto variable x is initialized to zero. When the function terminates, its value of 1 is lost.

An external static variable is declared outside of all functions and is available to all the functions in that program. The difference between a static external variable and a simple external variable is that the static external variable is available only within the file where it is defined while the simple external variable can be accessed by other files.

It is also possible to control the scope of a function. For example, we would like a particular function accessible only to the functions in the file in which it is defined, and not to any function in other files. This can be accomplished by defining 'that' function with the storage class static.

## Register Variables

We can tell the compiler that a variable should be kept in one of the machine's registers, instead of keeping in the memory (where normal variables are stored). Since a register access is much faster than a memory access, keeping the frequently accessed variables (e.g., loop control variables) in the register will lead to faster execution of programs. This is done as follows:

```
register int count;
```

Although, ANSI standard does not restrict its application to any particular data type, most compilers allow only int or char variables to be placed in the register. Since only a few variables can be placed in the register, it is important to carefully select the variables for this purpose. However, C automatically converts register variables into nonregister variables once the limit is reached.

## Table 10.1 Scope and Lifetime of Declarations

| Storage class | Where declared | Visibility (Active) | Lifetime (Active) |
|---|---|---|---|
| None | Before all functions in a file (may be initialized) | Entire file plus other files where variable is declared with extern. | Entire program (Global) |
| extern | Before all functions in a file (cannot be initialized) | Entire file plus other files where variable is declared extern and the file where originally declared as global. | Global |
| static | Before all functions in a file | Only in that file | Global |
| None or auto | Inside a function (or a block) | Only in that function or block | Until end of function or block |
| register | Inside a function or block | Only in that function or block | Until end of function or block |
| static | Inside a function | Only in that function | Global |

## 10.16 ANSI C FUNCTIONS

## Function Definition

As mentioned in the beginning of this chapter, ANSI standard combines the function definition and arguments declaration in one line (the function header). The general form of ANSI C functions is:

```
data-type function-name (type1 a1, type2 a2... typeN aN)
{
    .....
    .... (body of the function)
    .....
}
```

Here data-type refers to the type of the value returned by the function function-name and type1, type2,..., typeN are types of arguments a1, a2,..., aN.

As usual, if no data type is specified for the function, then, by default, the function is assumed to return an integer value. The arguments declaration is done using the comma separator. Remember, each argument must be independently declared with type specifier and name. That is, similar type arguments cannot be combined under one type name, like variable declarations. For example,

```
double funct(int a, int b, double c)
```

is a valid function definition, whereas

```
double funct(int a, b, double c)
```

is incorrect.

This new version of function definition, which combines the argument list and the arguments declaration, is called a function prototype. Function prototypes were not part of the original C language. It is one of the important recommendations of the ANSI C committee.

## Function Declaration

We know that every function that is being referenced should be declared for its type in the calling function. For example:

```
main()
{
    float a, b, x;
    float mul(); /* function declaration (old type) */
    ....
    ....
    x = mul(a,b); /* function call */
}
```

Note that the function declaration as stated above specifies the type of value returned by the function mul and does not talk anything about its arguments. The actual arguments are specified only when the function is called.

The introduction of "function prototypes" requires that the function declaration must include not only the type of return value but also the type and number of arguments to expect. Above program segment may be modified using the function prototype as follows:

```
main()
{
    float a, b, x;
    float mul(float a, float b);  /* function prototype */
    ....                       /* ANSI declaration */
    x = mul(a, b);
}
```

The general form of function declaration using ANSI prototype is:

```
data-type function-name (type1 a1, type2 a2, .... typeN aN);
```

One major reason for using function prototypes in function declarations is that they enable the compiler check for any mismatch of type and number of arguments between the function calls and the function definitions. They also help the compiler to perform automatic type conversions on function parameters. When a function is called, the actual arguments are automatically converted to the types in the function definition using the normal rules of assignment.
