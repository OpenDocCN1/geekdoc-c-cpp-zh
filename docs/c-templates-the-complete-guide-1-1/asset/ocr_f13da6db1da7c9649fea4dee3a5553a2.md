```
```cpp
// declares in namespace std:
template<typename T, typename Allocator = allocator<pair<const T, T>>>
class map;
// namespace std
template<typename T, typename Allocator = allocator<pair<const T, T>>>
class multimap;
template<typename T, class Allocator = allocator<T>>
class vector;
```
```

```
```cpp
template<typename T,
         class Allocator = allocator<T>>
class C {
  ...
};
```
```

```
```cpp
class AnotherClass;

namespace N {
  class AnotherClass;
}
```
```

```
```cpp
template<typename T, typename Allocator = allocator<T>>
class C;

// error: no default argument in declaration
template<typename T, class Allocator = allocator<T>>
class C;
```
```

The fact that a parameter of C++ only has a default if it is used in a declaration template parameter does not indicate that only class templates declared with the keyword class are allowed to be substituted as arguments. Indeed, struct, union, and class templates are all valid arguments for a template parameter (template parameters also accept built-in types, pointer types, and so on). This is similar to the observation that any type can be used as a template parameter, whether declared with the keyword class or not.

# ### 3.2.3.5 Equivalence

Two sets of template arguments are equivalent when the values of the arguments are identical for one or more types. For instance, `template<typename T, int N>` and `template<class T, int N>` are equivalent.

Click here to view code image

```
```cpp
template<typename T, int N>
class C;

C<int, 5> x;       // ok
C<int, 5> y;       // ok
C<int, 5> z;       // ok
```
```

To be clear in this example, no definition is needed to establish the equivalence of a template argument list.

In a template-dependent context, however, the “value” of a template argument cannot always be established definitively, and the rules for equivalence become a little more complicated. Consider the following example:

Click here to view code image

```
```cpp
template<typename T, int N>
class C;

C<int, 5> x;       // ok
C<int, 5> y;       // ok
C<int, 5> z;       // ok
```
```

Only declarations of `N` are exactly equivalent, and not just the declarations for `x`, `y`, and `z` (respectively), and not just the declaration `template<typename T, int N>`. Thus the two declarations are equivalent and define the same function template.

Declarations of `x`, `y`, and `z` are not equivalent. In particular, the declaration of `x` and the declaration of `y` are not equivalent. The declaration of `z` and the declaration of `x` are not equivalent. The declaration of `y` and the declaration of `z` are not equivalent.

A function generated from a function template is never equivalent to an ordinary function even though they may have the same name and the same type. This has two important consequences for class members:

+   1. A function generated from a member function template never overrides a virtual function.
+   2. A constructor generated from a constructor template is never a copy constructor. Similarly, an assignment generated from an assignment template is never a copy-assignment or a move-assignment operator. (However, this is less prone to problems because implicit calls of copy-assignment or move-assignment operators are less common.)

This is also good and bad. See Section 13.2 on page 632 and Section 5.4 on page 102 for details.

# ### 3.2.4 VARIADIC TEMPLATES

Variadic templates, introduced in Section 3.1 on page 35, are templates that can take a variable number of template parameters (see Section 3.1.2 on page 37).