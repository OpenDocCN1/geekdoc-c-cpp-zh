If you don't complicate the basic idea that a pointer is a variable whose value is a memory address then you have the foundation for understanding and using pointers in EMBOSS.

# Example

Consider the following code:

```
int main()
{
        ajint x=0;
/* 1. */      printf("Value of x : %d\n", x);
/* 2. */      printf("Memory address of x : %p\n", &x);
/* 3. */      printf("Value of x by indirection : %d\n", *(&x) );
}
/* Output will look like:
Value of x : 0
Memory address of x : #1
Value of x by indirection : 0
(In reality, a hexadecimal number would be printed instead of '#1',
but '#1' is easier to follow).
*/
```

The variable name x is our handle on the reserved memory. It refers to an integer value that resides at memory address #1. In the code the following is done:

+   1. First print the value of x.
+   2. Then use & to get the memory address of variable x and print it.
+   3. Then use the * operator to dereference this address and print the value stored there.

# 5.2.1.1 Declaring pointers

In practice a pointer holds the memory address of a specific object such as an integer, C data structure or even another pointer. The type of data pointed at must be specified when the pointer is declared. This is not because the memory address of an int is any different to that of a float, it's so that the compiler knows how the pointer can be used in the source code. For instance the compiler must know the type of data pointed at to be able to access the memory pointed at in order to, for example, print a value correctly. This is why in C pointers are declared in the manner shown:

```
ajint *ptr=NULL;
```

The * in the declaration means that ptr is a memory address and the ajint tells us that it's the address of an integer, i.e. ptr is a pointer to an integer.

When that line of the program is executed, sufficient memory to hold a memory address will be reserved for use by our program. This, like an integer, is normally 4 bytes on 32-bit machines. The value of these 4 bytes is set to NULL.