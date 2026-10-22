
```
int main()
{
int a;
clear(a); // ERROR: int doesn't support the unary *
}
```

## 12.3.3 Nontype Arguments

Nontype template arguments are the values substituted for nontype parameters. Such a value must be one of the following things:
- Another nontype template parameter that has the right type.
- A compile-time constant value of integer (or enumeration) type. This is acceptable only if the corresponding parameter has a type that matches that of the value or a type to which the value can be implicitly converted without narrowing. For example, a char value can be provided for an int parameter, but 500 is not valid for an 8-bit char parameter.
- The name of an external variable or function preceded by the built-in unary & (“address of”) operator. For functions and array variables, & can be left out. Such template arguments match nontype parameters of a pointer type. C++17 relaxed this requirement to permit any constant-expression that produces a pointer to a function or variable.
- The previous kind of argument but without a leading & operator is a valid argument for a nontype parameter of reference type. Here too, C++17 relaxed the constraint to permit any constant-expression glvalue for a function or variable.
- A pointer-to-member constant; in other words, an expression of the form &C::m where C is a class type and m is a nonstatic member (data or function). This matches nontype parameters of pointer-to-member type only. And again, in C++17, the actual syntactic form is no longer constrained: Any constant-expression evaluating to a matching pointer-to-member constant is permitted.
- A null pointer constant is a valid argument for a nontype parameter of pointer or pointer-to-member type.

For nontype parameters of integral type—probably the most common kind of nontype parameter— implicit conversions to the parameter type are considered. With the introduction of constexpr conversion functions in C++11, this means that the argument before conversion can have a class type.
Prior to C++17, when matching an argument to a parameter that is a pointer or

either.) One of the problems with string literals is that two identical literals can be stored at two distinct addresses. An alternative (but cumbersome) way to express templates instantiated over constant strings involves introducing an additional variable to hold the string: Click here to view code image

```
template<char const* str>
class Message {
...;
};

extern char const hello[] = "Hello World!";
char const hello11[] = "Hello World!";

void foo()
{
static char const hello17[] = "Hello World!";

Message<hello> msg03; // OK in all versions
Message<hello11> msg11; // OK since C++11
Message<hello17> msg17; // OK since C++17
}
```

The requirement is that a nontype template parameter declared as reference or pointer can be a constant expression with external linkage in all C++ versions, internal linkage since C++11, or any linkage since C++17.

See Section 17.2 on page 354 for a discussion of possible future changes in this area Here are a few other (less surprising) invalid examples: Click here to view code image

```
template<typename T, T nontypeParam>
class C;

struct Base {
int i;
} base;

struct Derived : public Base {
} derived;

C<Base*, &derived>* err1; // ERROR: derived-to-base conversions are not considered

C<int&, base.i>* err2; // ERROR: fields of variables aren’t considered to be variables

int a[10];
C<int*, &a[0]>* err3; // ERROR: addresses of array elements aren’t acceptable either
```

## 12.3.4 Template Template Arguments

A template template argument must generally be a class template or alias template with parameters that exactly match the parameters of the template template parameter it substitutes. Prior to C++17, default template arguments of a template template argument were ignored (but if the template template parameter has default arguments, they are considered during the instantiation of the template). C++17 relaxed the matching rule to just require that the template template parameter be at least as specialized (see Section 16.2.2 on page 330) as the corresponding template template argument.

This makes the following example invalid prior to C++17: Click here to view code image

```
#include <list>
// declares in namespace std:
// template<typename T, typename Allocator = allocator<T>>
// class list;

template<typename T1, typename T2,
template<typename> class Cont> // Cont expects one parameter
class Rel {
... 
};

Rel<int, double, std::list> rel; // ERROR before C++17: std::list has more than
// one template parameter
```

The problem in this example is that the std::list template of the standard library has more than one parameter. The second parameter (which describes an allocator) has a default value, but prior to C++17, that is not considered when matching std::list to the Container parameter.

Variadic template template parameters are an exception to the pre-C++17 “exact match” rule described above and offer a solution to this limitation: They enable more general matching against template template arguments. A template template parameter pack can match zero or more template parameters of the same kind in the template template argument: Click here to view code image

```
#include <list>

template<typename T1, typename T2,
template<typename...> class Cont> // Cont expects any number of
class Rel { // type parameters
...
};
```

```
Rel<int, double, std::list> rel; // OK: std::list has two template parameters
// but can be used with one argument
```

Template parameter packs can only match template arguments of the same kind. For example, the following class template can be instantiated with any class template or alias template having only template type parameters, because the template type parameter pack passed there as TT can match zero or more template type parameters: Click here to view code image

```
#include <list>
#include <map>
// declares in namespace std:
// template<typename Key, typename T,
// typename Compare = less<Key>,
// typename Allocator = allocator<pair<Key const, T>>>
// class map;
#include <array>
// declares in namespace std:
// template<typename T, size_t N>
// class array;
```

```
template<template<typename... > class TT>
class AlmostAnyTmpl {
};
```

```
AlmostAnyTmpl<std::vector> withVector; //two type parameters
AlmostAnyTmpl<std::map> withMap; // four type parameters
AlmostAnyTmpl<std::array> withArray; // ERROR: a template type parameter pack
// doesn’t match a nontype template parameter
```

The fact that, prior to C++17, only the keyword class could be used to declare a template template parameter does not indicate that only class templates declared with the keyword class were allowed as substituting arguments. Indeed, struct, union, and alias templates are all valid arguments for a template template parameter (alias templates since C++11, when they were introduced). This is similar to the observation that any type can be used as an argument for a template type parameter declared with the keyword class.

## 12.3.5 Equivalence

Two sets of template arguments are equivalent when values of the arguments are identical one-for-one. For type arguments, type aliases don’t matter: It is the type

ultimately underlying the type alias declaration that is compared. For integer nontype arguments, the value of the argument is compared; how that value is expressed doesn’t matter. The following example illustrates this concept: Click here to view code image

```
template<typename T, int I>
class Mix;

using Int = int;

Mix<int, 3*3>* p1;
Mix<Int, 4+5>* p2; // p2 has the same type as p1
```

(As is clear from this example, no template definition is needed to establish the equivalence of the template argument lists.) In template-dependent contexts, however, the “value” of a template argument cannot always be established definitely, and the rules for equivalence become a little more complicated. Consider the following example: Click here to view code image

```
template<int N> struct I {};

template<int M, int N> void f(I<M+N>); // #1
template<int N, int M> void f(I<N+M>); // #2

template<int M, int N> void f(I<N+M>); // #3 ERROR
```

Study declarations #1 and #2 carefully, and you’ll notice that by just renaming M and N to, respectively, N and M, you obtain the same declaration: The two are therefore *equivalent* and declare the same function template f. The expressions M+N and N+M in those two declarations are called *equivalent*.

Declaration #3 is, however, subtly different: The order of the operands is inverted. That makes the expression N+M in #3 *not* equivalent to either of the other two expressions. However, because the expression will produce the same result for any values of the template parameters involved, those expressions are called *functionally equivalent*. It is an error for templates to be declared in ways that differ only because the declarations include functionally equivalent expressions that are not actually equivalent. However, such an error need not be diagnosed by your compiler. That’s because some compilers may, for example, internally represent N+1+1 in exactly the same way as N+2, whereas other compilers may not. Rather than impose a specific implementation approach, the standard allows either one and requires programmers to be careful in this area.

A function generated from a function template is never equivalent to an ordinary function even though they may have the same type and the same name. This has two important consequences for class members: 1. A function generated
