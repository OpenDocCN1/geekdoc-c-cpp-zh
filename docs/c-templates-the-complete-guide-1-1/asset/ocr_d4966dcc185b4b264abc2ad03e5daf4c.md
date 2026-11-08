# Chapter 6

# Move Semantics and enable_if<>

One of the most prominent features C++11 introduced was move semantics. You can use it to optimize copying and assignments by moving ("stealing") internal resources from a source object to a destination object instead of copying those contents. This can be done provided the source no longer needs its internal values or state (because it is about to be discarded).

Move semantics has a significant influence on the design of templates, and special rules were introduced to support move semantics in generic code. This chapter introduces these features.

# 6.1 PERFECT FORWARDING

Suppose you want to write generic code that forwards the basic property of passed arguments:

+   - Modifiable objects should be forwarded so that they still can be modified.
+   - Constant objects should be forwarded as read-only objects.
+   - Movable objects (objects we can "steal" from because they are about to expire) should be forwarded as movable objects.

To achieve this functionality without templates, we have to program all three cases. For example, to forward a call of f() to a corresponding function using ...

**Click here to view code image**

basic/forward.cpp

```
```cpp
#include <utility>
#include <iostream>

class X
{
};

void g (X& x)
{
  std::cout << "lvalue for variable\n";
}

void g (X const& x)
{
  std::cout << "lvalue for constant\n";
}

void g (X&& x)
{
  std::cout << "rvalue for movable object\n";
}

// let f() forward argument val to g():

void f (X& val)        // val is non-const lvalue => ...
{
  g(val);
}

void f (X const& val)
```
```