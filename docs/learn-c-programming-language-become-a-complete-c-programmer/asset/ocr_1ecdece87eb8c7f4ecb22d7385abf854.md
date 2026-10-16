```
f(d); // fisbound to f(int)
return g(t,d); // gmight be bound to g(X,int) }
auto x1 = ff(N::X{},1.1); // ff<N::X,double>; maybind g to N::g(X,int), narrowing 1.1 to 1
```

```
Namespace N {
double g(X,double);
}
```

// reopen N to takecare of doubles

```
auto x2 = ff(N::X,2.2); // ff<N::X,double>; binds g to N::g(X,double); the best match
```

# Section 26.3.4 Multiple Instantiation Points 753

For ff() we have two instantiation points. For the first call, we could generate the specialization at the initialization of x1 and get g(N::X,int) called. Alternatively, we could wait and generate the specialization at the end of the translation unit and get g(N::X,char) called. Consequently, the call ff(N::X{},1.1) is an error.

It is sloppy programming to call an overloaded function between two of its declarations. However, looking at a large program, a programmer would have no reason to suspect a problem. In this particular case, a compiler could catch the ambiguity. However, similar problems can occur in separate translation units, and then detection becomes much harder (for both compilers and programmers). An implementation is not obliged to catch problems of this kind.

To avoid surprising name bindings, try to limit context dependencies in templates.

# 26.3.5 Templates and Namespaces

When a function is called, its declaration can be found even if it is not in scope, provided it is declared in the same namespace as one of its arguments (§14.2.4). This is important for functions called in template definitions because it is the mechanism by which dependent functions are found during instantiation. The binding of dependent names is done (§iso.14.6.4.2) by looking at

+   [1] the names in scope at the point where the template is defined, plus
+   [2] the names in the namespace of an argument of a dependent call (§14.2.4). For example:

```
namespace N {
class A {/*...*/}; char f(A);
}
char f(int);
```

```
template<typename T> char g(T t)
{
return f(t); }
// choose f() depending on what T is
```