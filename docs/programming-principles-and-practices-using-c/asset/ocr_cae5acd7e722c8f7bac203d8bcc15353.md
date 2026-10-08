```
```cpp
        cout << "pi==" << pi << "; contents of pi==" << *pi << "\n";
        cout << "pd==" << pd << "; contents of pd==" << *pd << "\n";
```
```

The output for `*pi` will be the integer **17** and the output for `*pd` will be the double **2.71828**. The output for **pi** and **pd** will vary depending on where the compiler allocated our variables **x** and **e** in memory. The notation used for the pointer value (address) may also vary depending on which conventions your system uses; hexadecimal notation (§A.2.1.1) is popular for pointer values.

The contents of operator (often called the *dereference* operator) can also be used on the left-hand side of an assignment:

```
```cpp
        *pi = 27;       // OK: you can assign 27 to the int pointed to by pi
        *pd = 3.14159;  // OK: you can assign 3.14159 to the double pointed to by pd
        *pd = *pi;      // OK: you can assign an int (*pi) to a double (*pd)
```
```

Note that even though a pointer value can be printed as an integer, a pointer is not an integer. “What does an **int** point to?” is not a well-formed question; **ints** do not point, pointers do. A pointer type provides the operations suitable for addresses, whereas **int** provides the (arithmetic and logical) operations suitable for integers. So pointers and integers do not implicitly mix:

```
```cpp
        int i = pi;        // error: can't assign an int* to an int
        pi = 7;            // error: can't assign an int to an int*
```
```

Similarly, a pointer to **char** (a **char\***) is not a pointer to **int** (an **int\***). For example:

```
```cpp
        char *pc = pi;     // error: can't assign an int* to a char*
        pi = pc;           // error: can't assign a char* to an int*
```
```

Why is it an error to assign **pc** to **pi**? Consider one answer: a **char** is usually much smaller than an **int**, so consider this:

```
```cpp
        char ch1 = 'a';
        char ch2 = 'b';
        char ch3 = 'c';
        char ch4 = 'd';
        int *pi = &ch3;   // point to ch3, a char-size piece of memory
                           // error: we cannot assign a char* to an int*
                           // but let's pretend we could
        *pi = 12345;      // write to an int-size piece of memory
        *pi = 67890;
```
```