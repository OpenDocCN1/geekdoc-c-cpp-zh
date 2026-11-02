# REVIEW EXERCISES

R7.1 Trace the following code. Assume that a and b are stored at 20300 and 20308. Your trace table should have entries for a, a, b, and p.

```
double a = 1000;
double b = 2000;
double* p = &a;
*p = 3000;
p = &b;
a = *p * 2;
```

R7.2 Trace the following code. Assume that a and b are stored at 20300 and 20308. Your trace table should have entries for a, a, b, p, and q.

```
double a = 1000;
double b = 2000;
double* p = &a;
double* q = &b;
*p = *q;
p = q;
*p = 3000;
```

R7.3 What does the following code print?

```
double a = 1000;
double b = 2000;
double* p = &a;
double* q = &p;
b = *q;
p = &b;
a = *p * *q;
cout << a << " " << b << endl;
```

R7.4 Explain the mistakes in the following code. Not all lines contain mistakes. Each line depends on the lines preceding it.

```
1 double a = 1000;
2 double* p = &a;
3 int* p = &a;
4 double* q;
5 *q = 2000;
6 int* r = nullptr;
7 *r = 3000;
```

R7.5 Suppose that a system allows the use of any string as a password, even the empty string. However, when a user connects to the system for the first time, no password has been assigned. Describe how you can use a string* variable and the nullptr pointer to distinguish unassigned passwords from empty ones.