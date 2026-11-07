# 9.18 **friend Functions and friend Classes**

A friend function has access to a class’s public and non-public members. A class may have as friends

+   - stand-alone functions,
+   - entire classes (and thus all their functions) or
+   - specific member functions of other classes.

This section presents a mechanical example of how a friend function works. In Chapter 11, Operator Overloading, Copy/Move Semantics and Smart Pointers, we’ll show friend functions that overload operators for use with objects of custom classes. You’ll see that sometimes a member function cannot be used to define certain overloaded operators.

# Declaring a friend

To declare a non-member function as a friend of a class, place the function prototype in the class definition and precede it with the keyword friend. To declare all member functions of an existing class ClassTwo as friends of class ClassOne, place in ClassOne’s definition a declaration of the form:

```
friend class ClassTwo;
```

# Friendship Rules

These are the basic friendship rules:

+   - **Friendship is granted, not taken**—For class B to be a friend of class A, class A must declare that class B is its friend.
+   - **Friendship is not symmetric**—If class A is a friend of class B, you cannot infer that class B is a friend of class A.
+   - **Friendship is not transitive**—If class A is a friend of class B and class B is a friend of class C, you cannot infer that class A is a friend of class C.

# friends Are Not Subject to Access Modifiers

Member access notions of `public`, `protected` (Chapter 10) and `private` do not apply to friend declarations, so friend declarations can be placed anywhere in a class definition. We prefer to place friend declarations first inside the class definition’s body and not precede them with any access specifier.

# Modifying a Class’s private Data with a friend Function

Figure 9.28 defines the free function modifyX as a friend of class Count (line 8), so modifyX can set Count’s private data member m_x.

```
```cpp
// fig09_28.cpp
// Friends can access private members of a class.
#include <format>
#include <iostream>
```
```

**Fig. 9.28** │ Friends can access private members of a class. (Part 1 of 2.)