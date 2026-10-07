# Chapter 7 Functions: C++'s Programming Modules

However, the function prototype does not require that provide names for the variables; a list of types is enough. The program in Listing 7.2 prototypes cheers() by using only the argument type:

```
void cheers(int); // okay to drop variable names in prototype
```

In general, you can include or exclude variable names in the argument lists for prototypes. The variable names in the prototype just as placeholders, so if you do use names, they don't have to match the names in the function definition.

# C++ Versus ANSI C Prototyping

ANSI borrowed prototyping from C++, but the two languages have some differences. The most important is that ANSI C, to preserve compatibility with classic C, made prototyping optional, whereas C++ makes prototyping mandatory. For example, consider the following function declaration:

```
void say_hi();
```

In C++, leaving the parentheses empty is the same as using the keyword void within the parentheses. It means the function has no arguments. In ANSI C, leaving the parentheses empty means you are declining to state what the arguments are. That is, it means you're forgetting the argument list. The C++ equivalent for not identifying the argument is to use ellipsis:

```
void say_bye(...); // C++ abdication of responsibility
```

Normally this use of an ellipsis is needed only for interfacing with C functions having a variable number of arguments, such as printf().

# What Prototypes Do for You

You've seen prototypes help the compiler. But what do they do for you? They greatly reduce the chance of program errors. In particular, prototypes ensure the following:

+   - The compiler correctly handles the function return value.
- The compiler checks that you use the correct number of function arguments.
- The compiler checks that you use the correct type of arguments. If you don't, it converts the arguments to the correct type, if possible.

We've already discussed how to correctly handle the return value. Let's look now at what happens when you use the wrong number of arguments. For example, suppose you make the following call:

```
double z = cube();
```

A compiler that doesn't use function prototyping lets this by. When the function is called, it looks where the cube() should have placed a number and whatever value happens to be there. This is how C worked for ANSI C borrowed prototyping