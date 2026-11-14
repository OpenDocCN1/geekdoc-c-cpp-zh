The syntax for a function pointer, given in Figure 7.25, is a little more complex and, perhaps, more confusing than that for the data pointer. With a little practice, the complexity will disappear.

```
Syntax
return type (* functionPointer) (<arg0, arg1, ..., argn>)
arg list may be empty
```

Figure 7.25 Declaring a Pointer to a Function

Let's look at a couple of examples to see what this means.

# EXAMPLE 7.16

We make the following function pointer declaration:

```
int (* intFuncPtr) (void);
```

We read the declaration in several steps:

# intFuncPtr

+   1. is a pointer to a function.
+   2. the function takes no arguments.
+   3. the function returns an int.

# intFuncPtr

The parentheses enclosing the pointer, intFuncPtr, are important and necessary. Without them, we would have a prototype for a function that takes no arguments and returns a pointer to an integer.

Let's try another one,

```
double (* doubleFuncPtr) (int, char);
```

We read the declaration in several steps:

# doubleFuncPtr

+   1. is a pointer to a function.
+   2. the function takes two arguments, one of type integer and the other of type char.
+   3. the function returns a double.

As with the variables in C, the name of a function is equivalent to its address in memory. More specifically, for a function an address is the location where the body of the function is stored. Thus, to initialize or assign to a function pointer, one simply writes the function's name on the right-hand side of an assignment operator.

# EXAMPLE 7.17

We first declare a function pointer and then a function to point to. After that, we simply make the assignment.

```
int (* intFuncPtr) ();        // declare a function pointer
int myFunction(void);         // declare a function
intFuncPtr = myFunction;      // point to the function
```