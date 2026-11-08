
### 9.2.3 Combining Multiple Policies and/or Traits

Combining more than one trait and policy doesn't entirely do away with having multiple template parameters. However, they do reduce their number to something manageable. An interesting question, then, is how to order such multiple parameters.

A simple strategy is to order the parameters according to the increasing likelihood that their default value will be selected. Typically, this would mean that the traits parameters follow the policy parameters because the latter are more often overridden in client code. (The reverse order may have been noted for this strategy in our development.)

If we are willing to add a significant amount of complexity to our code, an alternative variant exists that essentially allows us to specify the nondefault algorithms in any order. Refer to Section 21.4 on page 523 for details.

### 9.2.4 Accumulation with General Iterators

Before we end this introduction to traits and policies, it is instructive to look at one version of `accumulate()` that adds the capability to handle generalized iterators (rather than just pointers), as expected from an industrial-strength generic component. Interestingly, this still allows us to be conformant with pointers because the C++ standard library provides iterator traits. (Traits are everywhere!) Thus, we could have defined our initial version of `accumulate()` as follows (ignoring our later refinements):

```cpp
#ifndef ACCUM_HPP
#define ACCUM_HPP

#include <iterator>

template<typename Iter>
auto accum (Iter start, Iter end)
{
    using VT = typename std::iterator_traits<Iter>::value_type;

    VT total{};  // assume this actually creates a zero

    while (start != end) {
        total += *start;
        ++start;
    }

    return total;
}

#endif // ACCUM_HPP
```

The `std::iterator_traits` structure encapsulates all the relevant properties of iterators. Because a partial specialization for pointers exists, these traits are conveniently used with any ordinary pointer types. Here is how a standard library implementation may implement this support:

```cpp
template<typename T>
struct iterator_traits<T*> {
    using difference_type = ptrdiff_t;
    using value_type = T;
    using pointer = T*;
    using reference = T&;
    using iterator_category = random_access_iterator_tag;
};
```

However, there is no type for the accumulation of values to which an iterator refers; hence we still need to design our own accumulation object.

## 9.3 TYPE FUNCTIONS

The initial traits example demonstrates that we can define behavior that depends on types. Traditionally, in C and C++, we define functions that could more specifically be called value functions. They take some values as arguments and return another value as a result. With templates, we can additionally define type functions: functions that take some type as arguments and produce a type or a constant as a result.

A very useful built-in type function is `sizeof`, which returns a constant describing the size (in bytes) of the given type argument. Class templates can also serve as type functions. The parameters of the type function are the template parameters, and the result is an instantiation of the class...

```cpp
// traits/sized.cpp
#include <cstddef>
#include <iostream>

template<typename T>
struct TypeSize {
    static std::size_t const value = sizeof(T);
};

int main()
{
    std::cout << "TypeSize<int>::value = "
              << TypeSize<int>::value << '\n';
}
```

This may not seem very useful, since we have the built-in `sizeof` operator available, but note that `TypeSize<int>` is a type, and it can therefore be passed as a class template argument itself. Alternatively, `TypeSize` is a template and can be passed as a template template argument.

In what follows, we develop a few more general-purpose type functions that can be used as traits classes in this way.

### 9.3.1 Element Types

Assume that we have a number of container templates, such as `std::vector<T>` and `std::list<T>`, as well as built-in arrays. We want a type function that, given such a container type, produces the element type. This can be achieved using partial specialization:

```cpp
// traits/elementtype.hpp
#include <vector>
#include <list>

template<typename T>
struct ElementType;                 // primary template

template<typename T>
struct ElementType<std::vector<T>> { // partial specialization
    using Type = T;
};

template<typename T>
struct ElementType<std::list<T>> { // partial specialization
    using Type = T;
};

...

template<typename T, std::size_t N>
struct ElementType<T[N]> { // partial specialization
    using Type = T;
};

...

template<typename T>
struct ElementType<T[]> { // partial specialization
    using Type = T;
};
```

Note that we should provide partial specializations for all possible array types.

```cpp
template<typename T>
class NoExceptType
{
public:
    explicit NoExceptType();
    explicit NoExceptType(const T&);
    explicit NoExceptType(T&&);
    ...
};
```

```cpp
template<typename T>
void printElementType(T const& t)
{
    std::cout << "Contains: "
              << typeid(typename ElementType<T>::Type).name()
              << std::endl;
}

int main()
{
    std::vector<int> c;
    printElementType(c);
    int arr[42];
    printElementType(arr);
}
```

The use of partial specialization allows us to implement the type function without requiring the container types to know about it. In many cases, however, the type function is designed along with the applicable types, and partial specialization is not required. For example, the standard library defines a type function `std::iterator_traits` (as the standard contains it), so we can write the following:

```cpp
template<typename T>
struct ElementType<T*>
{
    using Type = T;
};
```

This is not the default implementation, and it does not include specializations for container types that do not have an appropriate type function defined.

Naturally, it is usually advisable to provide member type definitions for class template parameters so that they can be accessed more easily in generic code (this is what standard container templates do). The following sketches the idea:

```cpp
template<typename T1, typename T2>
class ElementType<T1,T2>
{
public:
    using Type1 = T1;
    using Type2 = T2;
};
```

How is a type function useful? It allows us to parameterize a template in terms of a container type without also requiring parameters for the element type and other characteristics. For example, instead of

```cpp
template<typename T, typename C = std::vector<T>>
class MyClass
{
    ...
};
```

which requires the element type to be specified explicitly, we can declare

```cpp
template<typename C, typename T = typename ElementType<C>::Type>
class MyClass
{
    ...
};
```

where the element type is determined from the type function.

Observe how a trait is implemented as an extension to existing types; that is, we do not define type functions for unrelated types and types of classes. This is not the case for the type function called a policy. It is used to define policies. ...

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_276_0.png)

```cpp
template<typename T>
using ElementType = typename Element<T>::Type;
```

Which allows us to further simplify the declaration of our elements above to

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_276_1.png)

```cpp
template<typename C>
ElementType<C> someElements (C const& c);
```

### 9.3.2 Transformation Traits

In addition to providing access to particular aspects of a main parameter type, traits can also perform transformations on types, such as adding or removing references or const and volatile qualifiers.

**Removing References**

For example, we can implement a RemoveReference<> trait that turns reference types into their underlying object or function types, and leaves nonreference types alone:

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_276_2.png)

traits/removeReference.hpp

```cpp
template<typename T>
struct RemoveReferenceT {
    using Type = T;
};

template<typename T>
struct RemoveReferenceT<T&> {
    using Type = T;
};

template<typename T>
struct RemoveReferenceT<T&&> {
    using Type = T;
};
```

Again, a convenience alias template makes the usage simpler:

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_276_3.png)

```cpp
template<typename T>
using RemoveReference = typename
    RemoveReferenceT<T>::Type;
```

Removing the reference from a type is typically useful when the type was derived using a construct that sometimes produces reference types, such as the special deduction rule for function parameters of type T&& discussed in Section 5.6 on page 277.

The C++ standard library provides a corresponding type trait std::remove_reference<T>, which is described in Section 12.4 on page 277.

**Adding References**

Similarly, we can take an existing type and create an lvalue or rvalue reference from it (along with the usual convenience alias templates):

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_276_4.png)

traits/addReference.hpp

```cpp
template<typename T>
struct AddLValueReferenceT {
    using Type = T&;
};

template<typename T>
using AddLValueReference = typename AddLValueReferenceT<T>::Type;

template<typename T>
struct AddRValueReferenceT {
    using Type = T&&;
};
```
