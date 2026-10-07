# ISO/IEC 9899:2011 (E)                               © ISO/IEC 2011 – All rights reserved

object P2, associated with block B2, then either the execution of B2 shall begin before
texecution of B, or the execution of B2 shall end prior to assignment. If these
requirements are not met, the behavior is undefined.

Here an execution of B means that portion of the execution of the program that would
correspond to the lifetime of an object with scalar type and automatic storage duration
associated with B.

A translator is free to ignore any or aliasing implications of uses of restrict.

EXAMPLE 1 The file scope declarations

```
int * restrict a;
int * restrict b;
extern int c[];
```

assert that if an object is accessed using one of a, b, or c, and that object is modified anywhere in the
program, then it is never accessed using either of the other.

EXAMPLE 2 The function parameter declarations in the following example

```
void f(int n, int *restrict p, int *restrict q)
{
    while (n-- > 0)
    *p++ = *q++;
}
```

assert that, during execution of the function, if object is accessed through one of the pointer
parameters, then it is not accessed through the other.

The benefit of the restrict qualifier is that they enable a translator to make an effective difference
analysis of function f without examining any of the calls of f in the program. The cost is that
programmer has to examine all of those calls to ensure no undefined behavior occurs. For example, the
second call of f in g has undefined behavior because of d[49] is accessed through
p p and q.

```
void g(void)
{
    extern int d[100];
    f(50, d + 50, d); // valid
    f(50, d + 1, d); // undefined behavior
}
```

EXAMPLE 3 The function parameter declarations
void h(int n, int *restrict p, int *restrict q, int *restrict r)

```
int i;
for (i = 0; i < n; i++)
    p[i] = q[i] + r[i];
```

illustrate how an undefined object can be accessed through two restricted pointers. In particular, if a and b
dis disjoint arrays, a call of the form h(100, a, b) has undefined behavior, because array is not
modified within function h.