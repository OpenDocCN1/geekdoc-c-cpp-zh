P2, associated with block B2, then either the execution of B2 shall begin before the execution of B, shall end prior to the assignment. If these requirements are not met, the behavior is undefined.

5 Here an execution of B means that portion of the execution of the program that would correspond to the lifetime of an object with scalar type and automatic storage duration associated with B.

6 A translator is free to ignore or all aliasing implications of uses of restrict.

7 EXAMPLE 1 The file scope declarations

```
int * restrict a;
int * restrict b;
extern int c[];
```

assert that an object is accessed using one a, b, or c, and that object is modified anywhere in the program, it is never accessed using either of the other two.

8 EXAMPLE 2 The function declarations in this example

```
void f(int n, int * restrict p, int * restrict q)
{
    while (n-- > 0)
        *p++ = *q++;
}
```

assert that, during each execution of the function, if an object is accessed through one of the pointer parameters, it is not accessed through the other.

9 The benefit of the restrict qualifiers is that they enable a translator to make an effective dependence analysis of function f without examining any of the calls of f in the program. The cost is that the programmer has to examine all of calls to ensure that no given undefined behavior. For example, the second call of f g has undefined behavior because each of d[1] through d[49] is accessed through both p and q.

```
void g(void)
{
    extern int d[100];
    f(50, d + 50, d); // valid
    f(50, d + 1, d); // undefined behavior
}
```

10 EXAMPLE 3 The function parameter declarations

```
void h(int n, int * restrict p, int * restrict q, int * restrict r)
{
    int i;
    for (int i = 0; i < n; i++)
        p[i] = q[i] + r[i];
}
```

illustrate how an unmodified object can aliased through two restricted pointers. In particular, if a and b are disjoint arrays, a call of the form h(100, a, b, b) has defined behavior, because array b is not modified within function h.