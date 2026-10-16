however, only ptr1 would be a pointer variable; ptr2 would be an ordinary double variable. To avoid making this mistake, we will normally use a separate declaration for each pointer variable:

```
double * ptr1;
double * ptr2;
```

# 15.1.1.1 Using typedef for Readability

An alternative notation that does not require the repeated use of the asterisk in pointer declarations is to use typedef to rename a type. For example, we could first declare

```
typedef int * IntPointer;
```

in Example 15.1 and then use IntPointer to declare the pointers:

```
IntPointer iPtr = &i,
    jPtr = &j,
    kPtr = &k;
```

Such declarations improve the readability of pointer declarations, especially when pointer parameters are being declared.

# 15.1.2 Basic Pointer Operations

C++ supports a variety of operations on pointers, including initialization, dereferencing, I/O, assignments, comparisons, and arithmetic. We examine each of these in turn.

# 15.1.2.1 Initialization

When a pointer variable is initialized to an address, as in

```
int * iPtr = &i;
```

that address must be the address of an object whose type is the same as the type to which the pointer points. The pointer is said to be bound to that type. For example, the declarations

```
double doubleVar;
int * iPtr = &doubleVar; // ERROR
```

will cause a compiler error, because an integer pointer can only store addresses of integer objects.

One important exception is that 0 can be assigned to any pointer variable. The value that results is called the null pointer value for that type and 0 is often called the null address. Thus, the declarations

```
char * cPtr = 0;
int * iPtr = 0;
double * dPtr = 0;
```