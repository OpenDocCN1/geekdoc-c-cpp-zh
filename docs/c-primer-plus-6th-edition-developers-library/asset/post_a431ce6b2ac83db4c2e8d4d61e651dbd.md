
becomes

```
#pragma use_bool "true" "false"
```

## Generic Selection (C11)

In programming, the term *generic programming* indicates code that is not specific to a particular type but which, once a type is specified, can be translated into code for that type. C++, for example, lets you create generic algorithms in the form of templates that the compiler can then use to instantiate code automatically for a specified type. C doesn’t have anything quite like that. However, C11 adds a new sort of expression, called a *generic selection expression*, that can be used to select a value on the basis of the type of an expression, that is, on whether the expression type is int, double, or some other type. The generic selection expression is not a preprocessor statement, but its usual use is a part of a #define macro definition that has some aspects of generic programming.

A generic selection expression looks like this:

```
_Generic(x, int: 0, float: 1, double: 2, default: 3)
```

Here _Generic is a new C11 keyword. The parentheses following _Generic contain several comma-separated terms. The first term is an expression, and each remaining item is a type followed by a colon followed by a value, such as float: 1. The type of the first term is matched to one of the labels, and the value of the whole expression is the value following the matched label. For example, suppose x in the preceding expression is a type int variable. Then the type of x matches the int: label, making 0 the value of the whole expression. If the type doesn’t match a label, the value associated with the default: label is used for the whole expression. A generic selection statement is a little like a switch statement, except that the type of an expression rather than the value of an expression is matched to a label.

Let’s look at an example combining a generic selection statement with a macro definition:

```
#define MYTYPE(X) _Generic((X),\
    int: "int",\
    float : "float",\
    double: "double",\
    default: "other"\
)
```

Recall that a macro has to be defined on one logical line, but you can use a \ to break the one logical line into multiple physical lines. In this case, the generic selection expression evaluates to a string. For example, the macro invocation MYTYPE(5) evaluates to the string "int" because the type for the value 5 matches the int: label. Listing 16.13 illustrates this macro further.

### Listing 16.13 The predef.c Program

```
// mytype.c

#include <stdio.h>

#define MYTYPE(X) _Generic((X),\
    int: "int",\
    float : "float",\
    double: "double",\
    default: "other"\
)

int main(void)
{
    int d = 5;

    printf("%s\n", MYTYPE(d));      // d is type int
    printf("%s\n", MYTYPE(2.0*d)); // 2.0* d is type double
    printf("%s\n", MYTYPE(3L));    // 3L is type long
    printf("%s\n", MYTYPE(&d));    // &d is type int *
    return 0;
}
```

Here is the output:

```
int
double
other
other
```

The final two instances of MYTYPE() use types without matching labels, so the default string is used. We could have used more type labels to extend the capabilities of the macro, but the example serves to illustrate how _Generic-based macros work.

When evaluating a generic selection expression, the program does not evaluate the first term; it only determines the type. And the only expression it does evaluate is the one with the matching label.

You can use _Generic to define macros that act like type-independent (“generic”) functions. The section later in this chapter about the math library provides an example.

## Inline Functions (C99)

Normally, a function call has overhead. That means it takes execution time to set up the call, pass arguments, jump to the function code, and return. As you’ve seen, you can use a macro to place code inline, thus avoiding that overhead. C99, borrowing from C++ (but not always exactly), added another approach, inline functions. From the name, you might expect that an inline function replaces a function call with inline code, but you would be misled. What the C99 and C11 standards actually say is this: “Making a function an inline function suggests that calls to the function be as fast as possible. The extent to which such suggestions are effective is implementation-defined.” So making a function an inline function may cause the compiler to replace the function call with inline code and/or perform some other sorts of optimizations, or it may have no effect.

There are different ways to create inline function definitions. The standard says that a function with internal linkage can be made inline and that the definition for the inline function must be in the same file in which the function is used. So a simple approach is to use the inline function specifier along with the static storage-class specifier. Usually, inline functions are defined before the first use in a file, so the definition also acts as a prototype. That is, the code would look like this:

```
#include <stdio.h>
inline static void eatline()    // inline definition/prototype
{
    while (getchar() != '\n')
        continue;
}

int main()
{
...
    eatline();                // function call
...
}
```

Seeing the inline declaration, the compiler could choose, for example, to replace the eatline() function call with the function body. That is, the effect could end up the same as if you had written this code instead:

```
#include <stdio.h>
inline static void eatline()    // inline definition/prototype
{
    while (getchar() != '\n')
        continue;
}

int main()
{
...
    while (getchar() != '\n')    // function call replaced
        continue;
...
}
```

Because an inline function doesn’t have a separate block of code set aside for it, you can’t take its address. (Actually, you can take the address, but then the compiler will generate a non-inline function.) Also, an inline function may not show up in a debugger.

An inline function should be short. For a long function, the time consumed in calling the function is short compared to the time spent executing the body of the function, so there is no great savings in time using an inline version.

For the compiler to make inline optimizations, it has to know the contents of the function definition. This means the inline function definition has to be in the same file as the function call. For this reason, an inline function ordinarily has internal linkage. Therefore, if you have a multifile program, you need an inline definition in each file that calls the function. The simplest way to accomplish this is to put the inline function definition in a header file and then include the header file in those files that use the function.

```
// eatline.h
#ifndef EATLINE_H_
#define EATLINE_H_
inline static void eatline()
{
    while (getchar() != '\n')
        continue;
}
#endif
```

An inline function is an exception to the rule of not placing executable code in a header file. Because the inline function has internal linkage, defining one in several files doesn’t cause problems.

C, unlike C++, also allows a mixture of inline definitions with external definitions (function definitions with external linkage). For example, a program has the following three files:

```
//file1.c
...
```

```
//file2.c
...
```

```
//file3.c
...
```

```
//file1.c
...
inline static double square(double);
double square(double x) { return x * x; }

int main()
{
    double q = square(1.3);
...
```

```
//file2.c
...
double square(double x) { return (int) (x*x); }
void spam(double v)
{
    double kv = square(v);
```

```
//file3.c
...
inline double square(double x) { return (int) (x * x + 0.5); }
void masp(double w)
{
    double kw = square(w);
...
```

One has an inline static definition, as before. One has an ordinary function definition, hence having external linkage. And one has an inline definition that omits the static qualifier.

What happens? The spam() function in file2.c uses the square() definition in that file. That definition, having external linkage, is visible to the other files, but main() in file1.c uses the local static definition of square(). Because this definition also is inline, the compiler may (or may not) optimize the coding, perhaps inlining it. Finally, for file3.c, the compiler is free to use either (or both!) the inline definition of file3.c or the external linkage definition from file2.c. If you omit static from an inline definition, as in file3.c, the inline definition is considered as an alternative that could be used instead of the external definition.

Note that GCC implemented inline functions prior to C99 using somewhat different rules, so the GCC interpretation of inline can depend on which compiler flags you use.

## _Noreturn Functions (C11)

When C99 added the inline keyword, that keyword became the sole example of a function specifier. (The keywords extern and static are termed storage-class specifiers and can be applied to data objects as well as to functions.) C11 adds a second function specifier, _Noreturn, to indicate a function that, upon completion, does not return to the calling function. The exit() function is an example of a _Noreturn function, for once exit() is called, the calling function never resumes. Note that this is different from the void return type. A typical void function does return to the calling function; it just doesn’t provide an assignable value.

The purpose of _Noreturn is to inform the user and the compiler that a particular function won’t return control to the calling program. Informing the user helps to prevent misuse of the function, and informing the compiler may enable it to make some code optimizations.

## The C Library

Originally, there was no official C library. Later, a de facto standard emerged based on the Unix implementation of C. The ANSI C committee, in turn, developed an official standard library,
