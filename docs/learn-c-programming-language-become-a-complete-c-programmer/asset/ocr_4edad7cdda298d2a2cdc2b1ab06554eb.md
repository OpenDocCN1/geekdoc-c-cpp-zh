base classes are preferred over functions potentially found based on the argument types (operators follow a different rule; §18.2.1, §18.2.5). For example:

```
namespace N {
struct S { int i };
void f(S);
void g(S);
void h(int);
}
```

# Section 14.2.4 Argument-Dependent Lookup 397

```
struct Base {
void f(N::S);
};

struct D : Base { void mf();

void g(N::S x) {
f(x); // call Base::f()
mf(x); // call D::mf()
h(1); // error :no h(int) available
}
};
```

In the standard, the rules for argument-dependent lookup are phrased in terms of associated namespaces (§iso.3.4.2). Basically:

+   - If an argument is a class member, the associated namespaces are the class itself (including its base classes) and the class’s enclosing namespaces.
+   - If an argument is a member of a namespace, the associated namespaces are the enclosing namespaces.
+   - If an argument is a built-in type, there are no associated namespaces.

Argument-dependent lookup can save a lot of tedious and distracting typing, but occasionally it can give surprising results. For example, the search for a declaration of a function f() does not have a preference for functions in a namespace in which f() is called (the way it does for functions in a class in which f() is called):

```
namespace N {
template<class T>
void f(T, int); // N::f()
class X { };
}
namespace N2 { N::X x;
void f(N::X, unsigned);
void g()
{
f(x,1); // calls N::f(X,int)
}
```