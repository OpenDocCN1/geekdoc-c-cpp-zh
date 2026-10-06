# ISO/IEC 14882:2017(E)

of the name being defined, provided that the entity defined was already declared in the namespace and the definition appears after the point of declaration in a namespace that encloses the declaration's namespace.
Example:

```
namespace Q {
    namespace V {
        void f();
        void V::f() { /* ... */ } // OK
        void V::g() { /* ... */ } // error: g() is not yet a member of V
        namespace V {
            void g();
        }
    }
}
namespace R {
void V::g() { /* ... */ } // error: g doesn't enclose Q
// end example
```

If a friend in a non-local class declares a class, function, class template or function template,⁷ the friend is a member of the innermost enclosing namespace. The friend declaration does not by make the name invisible to lookup (6.4.1) [Note: If a matching declaration is provided at namespace scope (either before or after the class definition grant friendship). — end note] If a function or function template is called, it may be found by the name the lookup considers from namespaces and classes associated with the point of call (6.4.3). If a friend declaration is either unqualified or not a template-id and the declaration is an elaborated-type not consider any scopes outside the innermost namespace. [Note: The other forms of friend declarations cannot declare a new member of the innermost enclosing namespace and thus follow the usual lookup rules. — end note] [Example:

```
// Assume f and g have not yet declared.
template <class T>
void f2(T);
namespace A {
class X {
    friend void f(X); // A::f(X) is a friend
    class V {
        friend void g(); // A::g is a friend
        friend void h(int); // A::h is a friend // h not considered
    }
    friend void f2<int>; // A::f2<int> is a friend
};
// A::f, A::g and A::h are not visible
X: {
    void g() { /* ... */ } // definition of A::g
    void f(X) { /* ... */ } // definition of A::f
    void h(int) { /* ... */ } // definition of A::h
}
// A::f, A::g and A::h are visible and known to friends
```

97 includes if the name of the class or function is unqualified.

©ISO/IEC 2017 – All rights reserved 181