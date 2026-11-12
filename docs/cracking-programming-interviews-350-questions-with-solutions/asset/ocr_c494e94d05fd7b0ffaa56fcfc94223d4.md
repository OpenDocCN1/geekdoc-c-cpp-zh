+   - if T is an rvalue reference to object type, the result is an xvalue.
+   - otherwise, the result is a prvalue.
+   - The static_cast operator shall not cast away constness.

# **Question 71**    static cast and base/derived

Is the following program valid?

# Program 8.58: static cast and base/derived

```
```cpp
#include <cassert>
#include <typeinfo>
struct A {};
int main()
{
    A a1;
    const A a2 = a1;
    assert(typeid(a1) == typeid(a2));
    assert(typeid(A) == typeid(const A));
    assert(typeid(A) == typeid(a2));
    assert(typeid(A) == typeid(const A&));
    assert(typeid(A) == typeid(const volatile A));
    assert(typeid(A) == typeid(volatile A&));
}
```
```

# Solution of Question 71

Yes because it produces lvalue to the original object.

Let us assume that B is a base class of D.
B can be cast to a reference of D if a valid standard conversion from a pointer to D to a pointer to B exists provided:

+   - B is neither a virtual base class of D nor
+   - a base class of a virtual base class of D

If the object of type B is actually a subobject of an object of type D, the result refers to the enclosing object of type D as illustrated by this example.

# **Question 72**    static cast and inaccessible base

Can static cast be used with private base classes?