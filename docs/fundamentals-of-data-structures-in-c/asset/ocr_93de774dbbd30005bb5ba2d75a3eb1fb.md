# ## 2.6 Initialization of Pointers

Like ordinary variables, a pointer variable can be initialized. Static and external (global) pointer variables are initialized with NULL by default. Automatic (local) pointer variables can be initialized either with NULL or with the address of some other variable, which is already defined.

For example the statement,

```
ptr = &i;
```

is called as **pointer initialization**, since the address of `i` is initialized to the pointer variable `ptr`. A pointer variable can be also initialized as an ordinary variable in declaration itself. For example,

int i, *ptr = &i;

is also valid, since `ptr` points to the value stored in the address of `i`.

# ## 2.7 Pointer Arithmetic

An interesting use of pointers is pointer arithmetic. The arithmetic operations that can be performed on pointers are addition and subtraction. You can use the increment (++) and decrement (--) operators on the size of the variable pointed by the pointer. For example if

```
ptr++;
```

is an integer pointer, the increment operation moves the pointer by two bytes (since an integer is two bytes long) from where it is previously pointed. Similarly, if `ptr` is a character pointer, the increment operation moves the pointer by one byte (since a character is one byte long) from where it is previously pointed. If a decrement operation is carried out on a pointer, the pointer moves backwards, depending upon the size of the variable pointed by the pointer.

For example, if

```
ptr--;
```

is a character pointer. The decrement operation moves the pointer backwards by one byte from where it is previously pointed. The expression,

```
ptr += 6;
```

increments the pointer by 6 elements of its type. Similarly, a pointer can be subtracted from an integer. Besides incrementation and decrementation of a pointer to an integer, you may also subtract one pointer from another pointer in order to find the number of elements of their type which seperates the two pointers. Other operations like multiplication and division of pointers are prohibited. You cannot add or subtract `float` or `double` type pointers from each other.