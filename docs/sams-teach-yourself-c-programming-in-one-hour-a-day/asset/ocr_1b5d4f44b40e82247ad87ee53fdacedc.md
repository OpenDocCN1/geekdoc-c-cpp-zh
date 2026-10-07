# Working with Pointers to Functions

Pointers to functions provide another way of calling functions. "Hold on," you might be thinking. "How can you have a pointer to a function? Doesn't a pointer hold the address where a variable is stored?”

Well yes and no. It's true that a pointer holds an address, but it doesn't have to be the address where a variable is stored. When your program runs, the code for each function is loaded into memory starting at a specific address. A pointer to a function holds the starting address of a function—its entry point.

Why use a pointer to a function? It provides a more flexible way of calling a function. It lets the program choose from several functions, selecting the one that is appropriate for the current circumstances.

# Declaring a Pointer to a Function

As with all C variables, you must declare a pointer to a function before using it. The general form of the declaration is as follows:

```
type (*ptr_to_func)(parameter_list);
```

This statement declares ptr_to_func as a pointer to a function that returns type and passes the parameters in parameter_list. Here are some more concrete examples:

```
int (*func1)(int x);
void (*func2)(double y, double z);
char (*func3)(char *p[]);
void (*func4)();();
```

The first line declares func1 as a pointer to a function that takes one int argument and returns a type int. The second line declares func2 as a pointer to a function that takes two double arguments and has a void return type (no return value). The third line declares func3 as a pointer to a function that takes an array of pointers to char as its argument and returns a type char. The final line declares func4 as a pointer to a function that doesn't take any arguments and has a void return type.

Why do you need parentheses around the pointer name? Why can't you write, for the first example:

```
int *func1(int x);
```

The reason has to do with the precedence of the indirection operator, *. It has a relatively low precedence, lower than the parentheses surrounding the parameter list. The declaration just given, without the first set of parentheses, declares func1 as a