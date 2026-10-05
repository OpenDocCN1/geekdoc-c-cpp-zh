```
extern int *;
extern int y[];
```

The first declares x to be a pointer to int; the second declares y to an array of int of unspecified size (an incomplete type), the storage for it is defined elsewhere.

# EXAMPLE 3 The following declarations demonstrate the compatibility rules for variably modified types.

```
extern int n;
extern int m;
void fcompat(void)
{
int a[n][m];
int (*p)[4][n+1];
int c[n][6][m];
int (*r)[x][n+1];
np = a; // invalid: not compatible because 4 != 6
r = c; // compatible, but defined only if
 // n == 6m and m == n+1
}
```

EXAMPLE 4 All declarations of variably modified (VM) types must be at either block scope or function prototype. Array objects declared with the _Thread_local, static, or extern storage-class specifier cannot have a variable length (VLA) type. However, an object declared with the static storage-class specifier can have a VM type (that is, a pointer to a VLA type). Finally, all identifiers declared with a VM type must be ordinary identifiers and cannot, therefore, members of structures or unions.

```
extern int n; // invalid: file scope VLA
int A[n]; // invalid: file scope VLA
extern int (*p2)[n]; // invalid: file scope VM
int B[100]; // invalid: file scope not VM
void fdmla(int m, int C[m]); // valid: VLA with prototype scope
void fla(int m, int C[m]) // valid: adjusted to auto pointer to VLA\{
typef int VLA[m]; // valid: block scope typedef
struct tag {
int (*y)[n]; // invalid: y not ordinary identifier
int z[n]; // invalid: z not ordinary identifier
};
int D[m]; // valid: auto VLA
static int E[m]; // invalid: static block scope VLA
extern int F[m]; // invalid: F has linkage and is VLA
int (*s)[m]; // valid: auto pointer to VLA
extern int (*r)[m]; // invalid: r has linkage and points to VLA
static int (*q)[m] = &B; // invalid: q is a static block pointer to VLA
}
```

Forward references: function declarators (6.7.6.3), function definitions (6.9.1), initialization (6.7.9).