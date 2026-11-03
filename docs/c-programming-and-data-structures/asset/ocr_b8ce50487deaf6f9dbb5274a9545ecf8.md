For an IBM PC, the length of various data types are as follows:

| Data type | Size |
|---|---|
| characters | 1 byte |
| integers | 2 bytes |
| floats | 4 bytes |
| long integers | 4 bytes |
| doubles | 8 bytes |

The number of bytes used to store various data types depends on the system and can be found by making use of the sizeof operator. For example, if x is a variable, then sizeof(x) returns the number of bytes needed for the variable. (Systems like Pentium use 4 bytes for storing integers and 2 bytes for short integers.)

# Rules of Pointer Operations

+   1. A pointer variable can be assigned the address of another variable.
+   2. A pointer variable can be assigned the values of another pointer variable.
+   3. A pointer variable can be initialized with NULL or zero value.
+   4. A pointer variable can be pre-fixed or post-fixed with increment or decrement operators.
+   5. An integer value may be added or subtracted from a pointer variable.
+   6. When two pointers point to the same array, one pointer variable can be subtracted from another.
+   7. When two pointers point to the objects of the same data types, they can be compared using relational operators.
+   8. A pointer variable cannot be multiplied by a constant.
+   9. Two pointer variables cannot be added.
+   10. A value cannot be assigned to an arbitrary address (i.e. &x = 10; is illegal).

# 6.10 POINTERS AND ARRAYS

When an array is declared, the compiler allocates a base address and sufficient amount of storage to contain all the elements of the array in contiguous memory locations. The base address is the location of the first element (index 0) of the array. The compiler also defines the array name as a constant pointer to the first element. Suppose we declare an array x as follows:

```
int x[5] = {1, 2, 3, 4, 5};
```

Suppose the base address of x is 1000 and assuming that each integer requires two bytes, the five elements will be stored as follows:

![](bbox=[0.22, 0.95, 0.85, 0.99])

The name x is defined as a constant pointer pointing to the first element, x[0] and therefore the value of x is 1000, the location where x[0] is stored. That is, x = &x[0] = 1000

If we declare p as an integer pointer, then we can make the pointer p to point to the array x by the following assignment:

```
p = x;
```