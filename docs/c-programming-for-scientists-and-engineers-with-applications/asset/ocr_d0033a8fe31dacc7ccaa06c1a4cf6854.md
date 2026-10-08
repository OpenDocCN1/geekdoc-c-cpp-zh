The arguments in a function call, in the prototype, and in the implementation header must match as number, order, and data type.

# 5.2.3 Scope of Names

In C every name has a scope, that is, the name is known and recognized within a particular section of the program. In the previous example, main and compute_area are global names. A name is local if its scope is a single function of a program. In the example, r, area, radius, and PI are local names. If a name is known to several functions, but not to all the functions, it is said to be “global” to those functions where it is known. In the example, area is not global—rather there are two variables named area, local to main and the other local to compute_area.

Whether a name is local or global depends on where it is declared. If a name is declared ahead of all the function definitions, including main(), it is global. Any function can access a name that is global to it. It can also access local names. But a function cannot access a name that is neither global to it or local.

```
int MAX;
FILE *inptr;
int gooddata(int, int, float);

int main() /* MAX, inptr, gooddata are global */
{
  ...
}
```

If a name is declared partway down a sequence of function definitions, it is “global to” to the functions that follow it.

```
void funcaccurate(float, float, float); /* funcaccurate is global */
int main()
{
  ...
}

const float limit = 0.0001; /* limit is global to funcaccurate */
/* can not be accessed by main */
void funcaccurate(float x, float y, float z)
{
  ...
}
```