![](bbox=[0.143, 0.104, 0.857, 0.238])

**Fig. 8.1** | Directly and indirectly referencing a variable.

Pointers, like any other variables, must be declared before they can be used. For example, for the pointer in Fig. 8.1, the declaration

```
```c
int *countPtr, count;
```
```

declares the variable countPtr to be of type int * (i.e., a pointer to an int value) and is read (right to left), “countPtr is a pointer to an int.” Also, variable count in the preceding declaration is declared to be an int, not a pointer to an int. The * in the declaration applies only to countPtr. Each variable being declared as a pointer must be preceded by an asterisk (*). For example, the declaration

```
```c
double *xPtr, *yPtr;
```
```

indicates that both xPtr and yPtr are pointers to double values. When * appears in a declaration, it isn’t an operator; rather, it indicates that the variable being declared is a pointer. Pointers can be declared to point to objects of any data type.

> > **Common Programming Error 8.1**
> >
> > Assuming that the * used to declare a pointer distributes to all variable names in a declaration’s comma-separated list of variable names can lead to error. Each pointer must be declared with the * prefixed to the name (either with or without spaces in between—the compiler ignores the space). Declaring only one variable per declaration helps avoid these types of errors and improves program readability.

> > **Good Programming Practice 8.1**
> >
> > Although it isn’t a requirement, including the letters Ptr in a pointer variable name makes it clear that the variable is a pointer and that it must be handled accordingly.

Pointers should be initialized either when they’re declared or in an assignment. A pointer may be initialized to 0, NULL or an address of the corresponding type. A pointer with the value 0 or NULL points to nothing and is known as a null pointer. Symbolic constant NULL is defined in header file <iostream> (and in several other standard library header files) to represent the value 0. Initializing a pointer to NULL is equivalent to initializing a pointer to 0, but in C++, 0 is used by convention. When 0 is assigned, it’s converted to a pointer of the appropriate type. The value 0 is the only integer value that can be assigned directly to a pointer variable without first casting the integer to a pointer type.

> > **Error-Prevention Tip 8.2**
> >
> > Initialize pointers to prevent pointing to unknown or uninitialized areas of memory.