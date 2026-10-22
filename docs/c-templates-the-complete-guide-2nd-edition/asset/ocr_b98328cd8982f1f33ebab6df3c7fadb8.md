```
};
void g (C<int>* p)
{
{ f(); // is f() visible here?
f(*p); // is f(C<int> const&) visible here?
}
```

If friend declarations were visible in the enclosing namespace, then instantiating a class template may make visible the declaration of ordinary functions. This would lead to surprising behavior: The call f() would result in a compilation error unless an instantiation of the class C occurred earlier in the program!

On the other hand, it can be useful to declare (and define) a function in a friend declaration only (see Section 21.2.1 on page 497 for a technique that relies on this behavior). Such a function can be found when the class of which they are a friend is among the associated classes considered by ADL.

Reconsider our last example. The call f() has no associated classes or namespaces because there are no arguments: It is an invalid call in our example. However, the call f(*p) does have the associated class C<int> (because this is the type of *p), and the global namespace is also associated (because this is the namespace in which the type of *p is declared). Therefore, the second friend function declaration could be found provided the class C<int> was actually fully instantiated prior to the call. To ensure this, it is assumed that a call involving a lookup for friends in associated classes actually causes the class to be instantiated (if not done already).³

The ability of argument-dependent lookup to find friend declarations and definition is sometimes referred to as friend name injection. However, this term is somewhat misleading, because it is the name of a pre-standard C++ feature that did in fact “inject” the names of friend declarations into the enclosing scope, making them visible to normal name lookup. In our example above, this would mean that both calls would be well-formed. This chapter’s aftersnotes further detail the history of friend name injection.

# 13.2.3 Injected Class Names

The name of a class is injected inside the scope of that class itself and is therefore accessible as an unqualified name in that scope. (However, it is not accessible as a qualified name because this is the notation used to denote the constructors.) For example: Click here to view code image