```
}
```

It may seem obvious to choose N2::f(), but that is not done. Overload resolution is applied and the best match is found: N::f() is the best match for f(x,1) because 1 is an int rather than an unsigned. Conversely, examples have been seen where a function in the caller’s namespace is chosen but the programmer expected a better function from a known namespace to be used (e.g., a standard-library function from std). This can be most confusing. See also §26.3.6.

# 14.2.5 Namespaces Are Open

A namespace is open; that is, you can add names to it from several separate namespace declarations. For example:

```
namespace A {
int f(); // now A has member f()
}
```

```
namespace A {
int g(); // now A has two members, f() and g()
}
```

That way, the members of a namespace need not be placed contiguously in a single file. This can be important when converting older programs to use namespaces. For example, consider a header file written without the use of namespaces:

```
// myheader

void mf(); // myfunction
void yf(); // your function
int mg(); // myfunction
// ...
```

Here, we have (unwisely) just added the declarations needed without concerns of modularity. This can be rewritten without reordering the declarations:

```
// myheader

namespace Mine { void mf(); // ...
}
// myfunction
void yf(); // your function (not yet put into a namespace)

namespace Mine { int mg();
// ...
}
// myfunction
```

When writing new code, I prefer to use many smaller namespaces (see §14.4) rather than putting really major pieces of code into a single namespace. However, that is often impractical when converting major pieces of software to use namespaces.