```
6  int* r = NULL;
7  *r = 3000;
```

**R7.5** Suppose that a system allows the use of any string as a password, even the empty string. However, when a user connects to the system for the first time, no password has been assigned. Describe how you can use a string* variable and the NULL pointer to distinguish unassigned passwords from empty ones.

**R7.6** Given the definitions

```
double primes[] = { 2, 3, 5, 7, 11, 13 };
double* p = primes + 3;
```

draw a diagram that explains the meanings of the following expressions:

+   a. `primes[1]`
+   b. `primes + 1`
+   c. `*(primes + 1)`
+   d. `p[1]`
+   e. `p + 1`

**R7.7** Suppose the array primes, defined as

```
double primes[] = { 2, 3, 5, 7, 11, 13 };
```

starts at memory location 20300. What are the values of

+   a. `primes`
+   b. `*primes`
+   c. `primes + 4`
+   d. `*(primes + 4)`
+   e. `primes[4]`
+   f. `&primes[4]`

**R7.8** Suppose the array primes is defined as

```
double primes[] = { 2, 3, 5, 7, 11, 13 };
```

Consider the sum function discussed in Section 7.2.3. What are the values of

+   a. `sum(primes, 6);`
+   b. `sum(primes, 4);`
+   c. `sum(primes + 2, 4);`
+   d. `sum(primes, 0);`
+   e. `sum(NULL, 4);`

**R7.9** Suppose the array primes, defined as

```
double primes[] = { 2, 3, 5, 7, 11, 13 };
```

starts at memory location 20300. Trace the function call `sum(primes, 4)`, using the definition of sum from Special Topic 7.2 on page 318. In your trace table, show the values for a, size, total, p, and i.

**R7.10** Pointers are addresses and have a numerical value. You can print out the value of a pointer as `cout << (unsigned)(p)`. Write a program to compare p, p + 1, q, and q + 1, where p is an `int*` and q is a `double*`. Explain the results.

**R7.11** A pointer variable can contain a pointer to a single variable, a pointer to an array, `NULL`, or a random value. Write code that creates and sets four pointer variables a, b, c, and d to show each of these possibilities.