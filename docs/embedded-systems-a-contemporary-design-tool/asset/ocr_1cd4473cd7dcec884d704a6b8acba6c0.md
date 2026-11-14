returns the proper number of bytes from memory whenever the pointer is dereferenced. It is occasionally convenient to be able to use the same pointer to refer to a variable of any type.

# generic pointer

To support such a capability, ANSI/ISO C introduces the generic pointer. The generic pointer is a pointer variable that can hold the address of a variable of any type. Such a pointer is said to be a pointer of type void or a void * pointer. Traditionally, this was done by casting the pointer to a variable of type pointer to char, then casting back to the proper type before dereferencing. The void * pointer was introduced to mitigate the obvious confusion that can result from using a char * pointer.

# void, void*

The void * pointer is guaranteed to be large enough to hold a pointer to any type of object, except a function type. A pointer to a variable of any type can be converted to a void* pointer and back again without losing any information.

An assignment to a void* pointer requires the use of the cast operator to remove the type information from the variable. To be able to dereference the value contained in the void* pointer, the process must be reversed; that is, the void* pointer must be cast back to a pointer of the original type. Because all of the type information has been taken away, a void* pointer cannot be dereferenced directly.

# EXAMPLE 7.13 Assigning to a generic pointer:

```
unsigned int* myIntPtr;       // declare a working pointer
void * myGenericPtr;          // declare a generic pointer
unsigned int myValue = 3;     // declare an integer variable
myGenericPtr = (void*) &myValue; // find the address of myValue and
                                // cast to a void*
```

To dereference the generic pointer, it must be cast back to a pointer of the original type. Dereferencing the generic pointer:

```
myIntPtr = (unsigned int*) myGenericPtr; // recast myGenericPtr back
                                         // to original type
```

# 7.3.4.2 Null Pointers

Recall that when a variable in C is declared and defined, no default value is automatically assigned. One certainly can dereference a pointer that has not been initialized or to which no specific value has been assigned. Dereferencing treats the pointer's value as an address; however, what the address is referring to is not known. It could refer to another part of the program, the operating system, or some other piece of code. Such bugs can be very difficult to find because, generally, the system will crash shortly after the errant dereference. Initializing values for global or static pointers vary with compiler vendor. The value 0 is typically used. Dereferencing such a value usually gives a runtime error followed by program termination. This is never a desirable result, but it is particularly unpleasant for embedded applications.

# null pointer

ANSI/ISO C offers a solution with the definition of a special pointer, the null pointer, whose value is guaranteed not to point to any object or function. That value is given as

```
(void*) 0
```

# <stddef.h>

and is defined as a macro in the header file <stddef.h>, where it is given the name NULL. Good programming style recommends that all pointers have the value NULL when not assigned to any object or function. The pointer must be assigned a valid address to some value before dereferencing.