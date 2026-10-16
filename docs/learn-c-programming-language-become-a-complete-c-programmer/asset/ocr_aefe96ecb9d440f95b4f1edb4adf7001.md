```
complex y {x}; // y also has the value {1,2} z=x; // z also has the value {1,2}
}
```

# 18.3.3.1 Conversions of Operands

We defined three versions of each of the four standard arithmetic operators:

```
complex operator+(complex,complex);
complex operator+(complex,double);
complex operator+(double ,complex);
// ...
```

This can get tedious, and what is tedious easily becomes error-prone. What if we had three alternatives for the type of each argument for each function? We would need three versions of each single-argument function, nine versions of each two-argument function, 27 versions of each three argument function, etc. Often these variants are very similar. In fact, almost all variants involve a simple conversion of arguments to a common type followed by a standard algorithm.

The alternative to providing different versions of a function for each combination of arguments is to rely on conversions. For example, our complex class provides a constructor that converts a double to a complex. Consequently, we could simply declare only one version of the equality operator for complex:

```
bool operator==(complex,complex);
```

```
void f(complex x, complex y) {
x==y; // means operator==(x,y)
x==3; // means operator==(x,complex(3))
3==y; // means operator==(complex(3),y)
}
```

There can be reasons for preferring to define separate functions. For example, in some cases the conversion can impose overhead, and in other cases, a simpler algorithm can be used for specific argument types. Where such issues are not significant, relying on conversions and providing only the most general variant of a function – plus possibly a few critical variants – contain the combinatorial explosion of variants that can arise from mixed-mode arithmetic.

Where several variants of a function or an operator exist, the compiler must pick “the right” variant based on the argument types and the available (standard and user-defined) conversions. Unless a best match exists, an expression is ambiguous and is an error (see §12.3).

An object constructed by explicit or implicit use of a constructor in an expression is automatic and will be destroyed at the first opportunity (see §10.3.4).
No implicit user-defined conversions are applied to the left-hand side of a . (or a->). This is the case even when the . is implicit. For example:

```
void g(complex z)
{
3+z; // OK: complex(3)+z
3.operator+=(z); // error :3isnot a class object
```