# # 57. Keep a type and its nonmember function interface in the same namespace.

# ## Summary

Nonmembers are functions too: Nonmember functions that are designed to be part of the interface of a class X (notably operators and helper functions) must be defined in the same namespace as the X in order to be called correctly.

# ## Discussion

Both public member functions and nonmember functions form part of the public interface of a class. The Interface Principle states: For a class X, all functions (including nonmember functions) that both “mention” X and are “supplied with” X in the same namespace are logically part of X, because they form part of X’s interface. (See Item 44 and [Sutter00].)

The C++ language is explicitly designed to enforce the Interface Principle. The reason why argument-dependent lookup (ADL, also known as Koenig lookup) was added to the language was to ensure that code that uses an object x of type X can use its nonmember function interface (e.g., cout << x, which invokes the nonmember operator<< for X) as easily as it can use member functions (e.g., x.f()), which requires no special lookup because f is clearly to be looked up in the scope of X). ADL ensures that nonmember functions that take X objects and that are supplied with X’s definition can participate as first-class members of X’s interface, just like X’s direct member functions naturally do.

In particular, the primary motivating example for ADL was the case where X is std::string (see [Sutter00]).

Consider a class X, defined in namespace N:

```
```cpp
class X {
public:
  void f();
};
X operator+( const X&, const X& );
```
```

Callers will typically want to write code like this, where x1, x2, and x3 are objects of type X:

```
```cpp
x3 = x1 + x2;
```
```