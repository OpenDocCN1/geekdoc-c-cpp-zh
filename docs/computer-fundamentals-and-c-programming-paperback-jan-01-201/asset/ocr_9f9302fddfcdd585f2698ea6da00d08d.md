![](bbox=[0.092, 0.136, 0.15, 0.177])

**Takeaway:** The preprocessor performs two tasks. First, it modifies the source code in accordance with the directives provided. Second, it removes all directives from the source code before it is passed on to the compiler.

# 17.2 #define: MACROS WITHOUT ARGUMENTS

The **#define** directive defines an alias for text that may be repeated in one or more programs. An alias is commonly known as a *macro* and in this section, we’ll discuss the macro in its simplest form—without arguments. The directive conforms to the following syntax:

```
```c
#define identifier replaced_text
```
```

When the preprocessor encounters a **#define** directive in a program, it makes a global replacement of *identifier* with *replaced_text*. Consider the following example that you have encountered before:

```
```c
#define PI 3.142
```
```

This directive replaces all instances of PI in the program with 3.142. The compiler thus sees only 3.142 and not PI. The constant 3.142 now has a name called PI and this macro is also called a *named constant, symbolic constant* or *defined constant*. We’ll mostly use these names to refer to a macro without arguments.

PI resembles a variable and uses the same naming convention (comprising letters, digits and underscores). For instance, YOUR_ANSWER and __TIME__ are valid names for symbolic constants. Although not mandatory, symbolic constants are usually defined in uppercase. It’s thus easy to distinguish them from variables which are normally defined in lowercase.

However, PI is not a variable and it is not assigned a value using the = operator. Furthermore, PI cannot be reassigned (say, to 3.142857 for greater precision) without first undefining it with **#undef**. (GCC simply issues a warning.) Here’s a code fragment that assigns PI twice in a program:

```
```c
#define PI 3.14                         No ; terminator
int main(void)
{
    printf("%f\n", PI);                Prints 3.140000
    #undef PI                           Must undefine PI ...
    #define PI 3.142857                  ... before redefining it
    printf("%f\n", PI);                Prints 3.142857
    ...
}
```
```

Note that preprocessor directives can be placed anywhere in a program even though they are normally bunched together at the beginning. Unlike with a variable, the scope of a named constant extends from the point of its definition to the end of the file. Thus, a named constant defined in a function is also visible in all subsequent functions; there are no “local” constants.

It’s easier to program using named constants than with the numbers and text they represent. For instance, the constant INR_USD is easier to remember than the number 64.65. If this constant