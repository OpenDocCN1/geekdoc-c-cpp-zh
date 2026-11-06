# 7.4 Dynamic Memory Allocation

> Use dynamic memory allocation if you do not know in advance how many values you need.

In many programming situations, you do not know beforehand how many values you need. To solve this problem, you can use *dynamic allocation* and ask the C++ run-time system to create new values whenever you need them. The run-time system keeps a large storage area, called the **heap**, that can allocate values and arrays of any type. When you ask for a

```
new double
```

then a storage location of type `double` is located on the heap, and a pointer to that location is returned. More usefully, the expression

> The new operator allocates memory from the heap.

```
new double[n]
```

allocates an array of size *n*, and yields a pointer to the starting element. (Here *n* need not be a constant.)
You will want to capture that pointer in a variable:

> You must reclaim dynamically allocated objects with the delete or delete[] operator.

```
double* account_pointer = new double;
double* account_array = new double[n];
```

You now use the pointer as described previously in this chapter. If you allocated an array, the magic of array/pointer duality lets you use the array notation `account_array[i]` to access the *i*th element.

When your program no longer needs memory that you previously allocated with the `new` operator, you must return it to the heap, using the `delete` operator:

```
delete account_pointer;
```

However, if you allocated an array, you must use the `delete[]` operator:

```
delete[] account_array;
```

This operator reminds the heap that the pointer points to an array, not a single value.

# Syntax 7.2 Dynamic Memory Allocation

![](bbox=[0.272, 0.641, 0.938, 0.928])