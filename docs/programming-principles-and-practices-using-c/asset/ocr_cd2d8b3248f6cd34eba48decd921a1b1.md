If an array is global, its elements will be initialized to the appropriate default value for the type. For example, the value of **a[7]** will be **0**. If the array is local (a variable declared in a function) or allocated using **new**, elements of built-in types will be uninitialized and elements of class types will be initialized as required by the class's constructors.

The name of an array is implicitly converted to a pointer to its first element. For example:

```
int* p = a;        // p points to a[0]
```

An array or a pointer to an element of an array can be subscripted using the **[ ]** operator. For example:

```
a[7] = 9;
int xx = p[6];
```

Array elements are numbered starting with 0; see §18.6.

Arrays are not range checked, and since they are often passed as pointers, the information to range check them is not reliably available to users. Prefer **vector**.

The size of an array is the sum of the sizes of its elements. For example:

```
int a[max];         // sizeof(a); that is, sizeof(int)*max
```

You can define and use an array of an array (a two-dimensional array), an array of an array of an array, etc. (multidimensional arrays). For example:

```
double da[100][200][300];        // 300 elements of type
                                   // 200 elements of type
                                   // 100 type double
da[7][9][11] = 0;
```

Nontrivial uses of multidimensional arrays are subtle and error-prone; see §24.4. If you have a choice, prefer a **Matrix** library (such as the one in Chapter 24).

# A.8.3 References

A *reference* is an alias (alternative name) for an object:

```
int a = 7;
int& r = a;
r = 8;   // a becomes 8
```