a prvalue is produced, a reference type would result in dangling references, but, fortunately, decltype(auto) will produce an object type (not a reference type) for that case.

Unlike auto, decltype(auto) does not allow specifiers or declarator operators that modify its type. For example: Click here to view code image

```
decltype(auto)* p = (void*)nullptr; // invalid
int const N = 100;
decltype(auto) const NN = N*N; // invalid
```

Note also that parentheses in the initializer may be significant (since they are significant for the decltype construct as discussed in Section 6.1 on page 91): Click here to view code image

```
int x;
decltype(auto) z = x; // object of type int
decltype(auto) r = (x); // reference of type int&
```

This especially means that parentheses can have a severe impact on the validity of return statements: Click here to view code image

```
int g();
...
decltype(auto) f() {
int r = g();
return (r); // run-time ERROR: returns reference to temporary
}
```

Since C++17, decltype(auto) can also be used for deducible nontype parameters (see Section 15.10.1 on page 296). The following example illustrates this: Click here to view code image

```
template<decltype(auto) Val> class S
{
...};
constexpr int c = 42;
extern int v = 42;
S<c> sc; // #1 produces S<42>
S<(v)> sv; // #2 produces S<(int&)v>
```

In line #1, the lack of parentheses around c causes the deducible parameter to be of the type of c itself (i.e., int). Because c is a constant-expression of value 42, this is equivalent to S<42>. In line #2, the parentheses cause decltype(auto) to become a reference type int&, which can bind to the global variable v of type int. Thus, with this declaration the class template depends on a reference to v, and any change of the value of v might impact the behavior of class S (see Section 11.4 on page 167 for details). (S<v> without