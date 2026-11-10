When the program was compiled and run, it produced the following output:

```
~~~
This sentence will
be printed
in multi-line
~~~
```

However if the string is too long to fit on a single line, then it is possible to spread a string over several lines by escaping the actual new-line character at the end of a line by preceding it with a backslash. The string may then be continued on the next line as shown in the following program:

```
~~~c
int main()
{
    printf("hello,\
world\n");
    return 0;
}
~~~
```

The output is

```
~~~
hello, world
~~~
```

The indenting spaces at the start of the string continuation have been taken as part of the string. A better approach is to use string concatenation which means that two strings which are only separated by whitespaces are regarded by the compiler as a single string. Space, newline, tab character, and comment are collectively known as whitespace. The use of string concatenation is shown by the following example:

```
~~~c
int main()
{
    printf("hello, " "world\n");
    return 0;
}
~~~
```

# 8.12.4 Assignment

The assignment operator is the single equal to sign (=). The general form of the assignment statement is

```
~~~c
variable_name = expression;
~~~
```

Some examples are given below.

```
~~~c
i = 6;
i = i + 1;
~~~
```

The assignment operator replaces the content of the location 'i' with the evaluated value of the expression on its right-hand side. The assignment also acts as an expression that returns the newly assigned value. Some programmers use the feature to write statements like the following:

```
~~~c
y = (x = 2 * x);
~~~
```

This statement puts x's new value in y. The operand to the left of the assignment operator must be a variable name. C does not allow any expression, constant, or function to be placed to the left of the assignment operator. Thus, its left

operand should be a variable and its right operand may be an arbitrary expression. The latter is evaluated and the outcome is stored in the location denoted by the variable name. For example, the mathematical expression x + 2 = 0 does not become an assignment expression in C by typing x + 2 = 0. It is wrong in C, as the left-hand side of the ‘equal to’ operator (assignment operator) must not have an expression, value, or constant.

The operand to the left of the assignment operator is an lvalue that denotes left value. An lvalue is anything that denotes a memory location in which a value may be stored. The only kind of lvalue identified so far in this book is a variable. It will be discussed in detail later in this chapter. Other types of lvalues, based on pointers and references, will be described later in the book.

# 8.12.5 Initialization

When a variable is declared, the C compiler does not assign any value to the variable, unless it is instructed to do so. Such declaration is called a tentative declaration. For example,

```
~~~c
int i; /* This declaration is tentative */
int x;
x = i + 5;
/* variable i is not assigned any known value, and
   therefore the value of x is undefined. This is a bug
*/
~~~
```

To prevent such pitfalls, always assign a value to the variable during the declaration of variables. This is known as initialization. The value of initialization is called the initializer. The general form of the initialization statement is

```
~~~c
data type variable_name=constant;
~~~
```

For example,

```
~~~c
int i = 100; /* 100 is an initializer */
int x;
x = i + 5;
/* since i has been given a value during its declaration,
   x is evaluated to hold a value 105 */
~~~
```

# Check Your Progress

+   1. What will be the output of the following program?

```
~~~c
(a) #include <stdio.h>
int main()
{
    int a=010;
    printf("\n a=%d",a);
    return 0;
}
~~~
```

Output a = 8

```
~~~c
(b) #include <stdio.h>
int main()
{
    int a=010;
~~~
```