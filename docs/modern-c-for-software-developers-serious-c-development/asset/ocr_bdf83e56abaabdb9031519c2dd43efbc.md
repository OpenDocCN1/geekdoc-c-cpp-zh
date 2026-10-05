# Modern C++: Move Semantics (C++11)

By default, copying an object in C++ involves doing a bit by bit copy of the object. This is called a deep copy. We can avoid making deep copies of objects by using references or copy constructors. In addition to this, another technique is available. Move semantics allows us to efficiently transfer resources from one object to another, without copying or using references or copy constructors.

# lvalues And rvalues

Every expression is either a lvalue (left value) or a rvalue (right value). A lvalue is a persistent value with an addressable location in memory. We can store values at this address on an ongoing basis. A rvalue is only stored transiently. A rvalue does not have an addressable memory location.

Historically, lvalues and rvalues are so called because a lvalue typically appears on the left-side of an assignment, whereas a rvalue appears only on the right side. If an expression is not an lvalue, it is a rvalue.

Consider the following example:

```
int result = std::abs(a*b)
```

The intermediate result a*b is a rvalue. It is a transient value that is not addressable. The return value of the function std::abs is also a rvalue. It is a transient value that exists until the assignment is completed. rvalues exist in memory for a transient period of time and cannot be addressed.

Note that the following assignment will generate a compiler error since a rvalue does not have an addressable location: