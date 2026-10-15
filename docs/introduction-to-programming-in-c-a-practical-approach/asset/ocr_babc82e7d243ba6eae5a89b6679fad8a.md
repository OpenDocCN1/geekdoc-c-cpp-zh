# 26.- Dynamic memory

In C we can reserve memory dynamically at run time.

In practice there are two types of memory: static memory managed by the compiler and dynamic memory managed by the programmer.

When defining variables, the compiler assigns them the necessary space depending on the type of the variable.

Depending on the scope where the variable is defined, the compiler allocates memory in the stack for local variables and function parameters.

For global variables, the compiler allocates the memory of the variables in a separate data segment.

The programmer can allocate memory dynamically at run time with the malloc function to which the number of bytes of the memory to be reserved is passed.

The reserved memory is created in a data segment HEAP used only for dynamic memory.

The malloc function returns a pointer to the reserved memory area.

E.g.

```
int *p = (int *) malloc (200);
```

The malloc function reserves 200 bytes of memory and returns an untyped pointer to the reserved zone.

An explicit casting is done to indicate that there are integers in the memory area.

The pointer p points to the reserved area with malloc.