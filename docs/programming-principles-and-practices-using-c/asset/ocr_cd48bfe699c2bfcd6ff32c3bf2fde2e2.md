# ### 17.3 Memory, addresses, and pointers

A computer’s memory is a sequence of bytes. We can number the bytes from 0 to the last one. We call such “a number that indicates a location in memory” an *address*. You can think of an address as a kind of integer value. The first byte of memory has the address 0, the next the address 1, and so on. We can visualize a megabyte of memory like this:

![](bbox=[0.22, 0.25, 0.68, 0.3])

Everything we put in memory has an address. For example:

```
`int var = 17;`
```

This will set aside an “int-size” piece of memory for **var** somewhere and put the value **17** into that memory. We can also store and manipulate addresses. An object that holds an address value is called a *pointer*. For example, the type needed to hold the address of an **int** is called a “pointer to int” or an “int pointer” and the notation is `int*`:

```
`int* ptr = &var;              // ptr holds the address of var`
```

The “address of” operator, unary **&**, is used to get the address of an object. So, if **var** happens to start at address **4096** (also known as $2^{12}$), **ptr** will hold the value **4096**:

![](bbox=[0.22, 0.61, 0.68, 0.66])

Basically, we view our computer’s memory as a sequence of bytes numbered from 0 to the memory size minus 1. On some machines that’s a simplification, but as an initial programming model of the memory, it will suffice.

Each type has a corresponding pointer type. For example:

```
`int x = 17;
int* pi = &x;                // pointer to int`
```

```
`double e = 2.71828;
double* pd = &e;             // pointer to double`
```

If we want to see the value of the object pointed to, we can do that using the “contents of” operator, unary **\***. For example: