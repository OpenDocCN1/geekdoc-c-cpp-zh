```
extern int max(a, b)
int a, b;
{
    return a > b ? a : b;
}
```

Here int a, b is the declaration list for the parameters. The difference between these two definitions is that the first form is a prototype declaration that forces conversion of the arguments of subsequent calls to the function, whereas the second form does not.

EXAMPLE 2 Pass one function to another, one might say

```
int f(void);
/* ... */
g(f);
```

Then the definition of g might read

```
void g(int (*funcp) void)
{
    /* ... */
    (*funcp)(); /* * or funcnp ((); ... * */
}
```

or, equivalently,

```
void g(int func(void))
{
    /* ... */
    func(); /* * or (*func) ((); ... * */
}
```

# 6.9.2 External object definitions

# Semantics

If the declaration of an identifier for an object has file scope and an initializer, the declaration is an external definition for the identifier.

A declaration of an identifier for an object that has file scope without an initializer, and without a storage-class specifier or with the storage-class specifier static, constitutes a tentative definition. If a translation unit contains one or more tentative definitions for an identifier, and the translation unit contains no external definition for that identifier, then the behavior is exactly as if the translation unit contains a file scope declaration of that identifier, with the composite type as the end of the translation unit, with an initializer equal to 0.

If the declaration of an identifier for an object is a tentative definition and has internal linkage, the declared type shall not be an incomplete type.