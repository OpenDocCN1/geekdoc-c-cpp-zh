Variables that are created during program execution are called **dynamic variables**. With the help of pointers, C++ creates dynamic variables. C++ provides two operators, `new` and `delete`, to create and destroy dynamic variables, respectively. When a program requires a new variable, the operator `new` is used. When a program no longer needs a dynamic variable, the operator `delete` is used.

In C++, `new` and `delete` are reserved words.

# Operator new

The operator `new` has two forms: one to allocate a single variable and another to allocate an array of variables. The syntax to use the operator `new` is:

```
new dataType;              // to allocate a single variable
new dataType[intExp];      // to allocate an array of variables
```

in which `intExp` is any expression evaluating to a positive integer.

The operator `new` allocates memory (a variable) of the designated type and returns a pointer to it—that is, the address of this allocated memory. Moreover, the allocated memory is uninitialized.

Consider the following declaration:

```
int *p;
char *q;
int x;
```

The statement:

```
p = &x;
```

stores the address of x in p. However, no new memory is allocated. On the other hand, consider the following statement:

```
p = new int;
```

This statement creates a variable during program execution somewhere in memory and stores the address of the allocated memory in p. The allocated memory is accessed via pointer dereferencing—namely, *p. Similarly, the statement:

```
q = new char[16];
```

creates an array of 16 components of type char and stores the base address of the array in q.