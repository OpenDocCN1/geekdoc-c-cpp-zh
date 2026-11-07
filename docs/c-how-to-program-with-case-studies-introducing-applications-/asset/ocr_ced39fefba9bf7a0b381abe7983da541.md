# ## 7.2 Pointer Variable Definitions and Initialization

Pointers are variables whose values are memory addresses. Usually, a variable *directly* contains a specific value. A pointer, however, contains the address of another variable that contains a specific value. The pointer *points to* that variable. In this sense, a variable name directly references a value, and a pointer indirectly references a value, as in the following diagram:

![](bbox=[0.3, 0.232, 0.83, 0.362])

Referencing a value through a pointer is called indirection.

# ### Declaring Pointers

Pointers, like all variables, must be defined before they can be used. The following statement defines the variable countPtr as an int *—a pointer to an integer:

```
```c
int *countPtr;
```
```

This definition is read right-to-left, “countPtr is a pointer to int” or “countPtr points to an object¹ of type int.” The * indicates that the variable is a pointer.

# ### Pointer Variable Naming

Our convention is to end each pointer variable’s name with *Ptr* to indicate that the variable is a pointer and should be handled accordingly. Other common naming conventions include starting the variable name with *p* (e.g., *pCount*) or *p_* (e.g., *p_count*).

# ### Define Variables in Separate Statements

The \* in the following definition does not distribute to each variable:

```
```c
int *countPtr, count;
```
```

so countPtr is a pointer to int, but count is just an int. For this reason, you should always write the preceding declaration as two statements to prevent ambiguity:

```
```c
int *countPtr;
int count;
```
```

# ### Initializing and Assigning Values to Pointers

Pointers should be initialized when they’re defined, or they can be assigned a value. A pointer may be initialized to NULL, 0 or an address:

+   1. In C, an “object” is a region of memory that can hold a value. So objects in C include primitive types such as ints, floats, chars and doubles, as well as aggregate types such as arrays and structs (which we discuss in Chapter 10).