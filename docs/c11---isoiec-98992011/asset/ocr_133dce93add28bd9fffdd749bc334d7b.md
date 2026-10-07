# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

```
extern int *x;
extern int y[];
```

The first declares x to be a pointer to int; the second declares y to be an array of int of unspecified size (an incomplete type), the storage for which is defined elsewhere.

+   9 EXAMPLE 3 The following declarations demonstrate the compatibility rules for variably modified types.

```
extern int n;
extern int m;
void fcomp(void)
{
int a[n] [6][m];
int (*p) [4] [n+1];
int c[n] [6][m];
int (*r) [n] [n+1];
p = a; // invalid: not compatible because 4 != 6
r = c; // compatible, but defined only if
n = 6 and m = n+1
}
```

+   10 EXAMPLE 4 All declarations of variably modified (VM) types have to be either at scope or prototype scope. Array objects declared with the Thread_local, static, or extern storage-class cannot have a variable length array (VLA) type. However, an object declared with the static storage-class can have a VM type (that is, a pointer to a VLA). Finally, all identifiers with a VM type must be ordinary identifiers and cannot, therefore, be members of structures or unions.

```
extern int n; // invalid: file scope VLA
int A[n]; // invalid: file scope VM
extern int (*p2) [n]; // invalid: file scope but not VM
int B[100];

void fla(int m, int C[m]); // valid: VLA with prototype scope
void fva(int m, int C[m]) // valid: adjusted to pointer to VLA
{
typedef int VLA[m][m]; // valid: block scope VLA
struct tag {
int (*y) [n]; // invalid: y not ordinary identifier
int z[n]; // invalid: z not ordinary identifier
}
 D[m]; // valid: auto VLA
static int E[m]; // valid: static block VLA
extern int F[m]; // invalid: F has linkage and is VLA
int (*s) [m]; // valid: auto pointer to VLA
extern int (*r) [m]; // invalid: r has linkage and points to VLA
static int (*q) [m] = &B; // valid: q is a static block pointer to VLA
}
```

Forward references: function declarations (6.7.6.3), function definitions (6.9.1), initialization (6.7.9).