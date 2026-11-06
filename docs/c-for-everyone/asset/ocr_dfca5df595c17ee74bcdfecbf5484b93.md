# Work with arrays and vectors of pointers.

# Draw diagrams for visualizing pointers and the data to which they point.

+   - Draw the data that is being processed, then draw the pointer variables. When drawing the pointer arrows, illustrate a typical situation.

![](bbox=[0.671, 0.153, 0.891, 0.209])

# Use structures to aggregate data items and work with pointers to structures.

![](bbox=[0.078, 0.249, 0.224, 0.287])

+   - A structure combines member values into a single value.
+   - You use the dot notation to access members of a structure.
+   - Use the -> operator to access a structure member through a pointer.

# REVIEW EXERCISES

**R7.1** Trace the following code. Assume that a and b are stored at 20300 and 20308. Your trace table should have entries for a, b, and p.

```
```cpp
double a = 1000;
double b = 2000;
double* p = &a;
*p = 3000;
p = &b;
a = *p * 2;
```
```

**R7.2** Trace the following code. Assume that a and b are stored at 20300 and 20308. Your trace table should have entries for a, b, p, and q.

```
```cpp
double a = 1000;
double b = 2000;
double* p = &a;
double* q = &b;
*p = *q;
p = q;
*p = 3000;
```
```

**R7.3** What does the following code print?

```
```cpp
double a = 1000;
double b = 2000;
double* p = &a;
double* q = p;
b = *q;
p = &b;
a = *p + *q;
cout << a << " " << b << endl;
```
```

**R7.4** Explain the mistakes in the following code. Not all lines contain mistakes. Each line depends on the lines preceding it.

```
```cpp
1   double a = 1000;
2   double* p = a;
3   int* p = &a;
4   double* q;
5   *q = 2000;
```
```