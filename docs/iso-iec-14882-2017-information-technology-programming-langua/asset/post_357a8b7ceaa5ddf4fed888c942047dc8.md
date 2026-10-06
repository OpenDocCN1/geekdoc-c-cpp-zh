
# ISO/IEC 14882:2017(E)

## 16.3.1 Initialization by conversion for direct reference binding

Under the conditions specified in 11.6.3, a reference can be bound directly to a value or clause value that is the result of applying a conversion function to an initializer expression. Overload resolution is used to select the conversion function invoked. "reference to cv T" is the type of the reference being initialized, and "cv S" is the type of the initializer, with S class type, the candidates are selected as follows:

- The conversion functions of S and its base classes are considered. These non-explicit conversion functions are not hidden within S and yield type "value reference to cv T2" (when initializing an rvalue reference to cv type) or "value reference to cv T2" (when initializing an rvalue reference or an rvalue reference to function), where "cv T" is reference-compatible (11.6.3) and "T2" are candidate functions. For-explicit conversion functions that are not hidden within S and yield type "value reference to cv T2" or "value reference to cv T2", respectively, where T2 is the same type as T or can be converted to a type with conversion (7,5), are also candidates.

The argument list has one match, which is the initializer. This argument will be considered against the object type of the conversion functions.

## 16.3.1.7 Initialization by list-initialization

When objects of class type are list-initialized, 11.6.4 specifies that overload resolution is performed according to the rules in this scope, overload resolution selects the constructor in two phases:

- Initially, the candidate functions are the list-initializer constructors of the class T and the argument list considers the list initializer as a single argument.

- If no list-initializer constructor is found, overload resolution is performed again, where the candidate functions are all the constructors of the class T and the argument list consists of the elements of the initializer list.

If the initializer has no elements and T has a default constructor, the initialization is ill-formed. [Note: This differs from other situations (16.3.1.3, 16.3.1.4), where only converting constructors are considered for copy-initialization. This restriction only applies if this initialization is part of the final result of overload resolution.]

## 16.3.1.8 Class template argument deduction

- A set of functions and function templates is formed comprising:

- For each constructor of the primary class template designated by the template-name, if the template is defined, a function template with the following properties:

    - The template parameters are the template parameters of the class template followed by the template parameters (including default template arguments) of the constructor, if

    - The return type is the class template specialization designated by the template-name and template arguments corresponding to the template parameters identified from the class template.

    - If the primary class C not define or declare any constructors, an additional function template derived as above from a hypothetical constructor CO().

    - An additional function template derived as above from a hypothetical constructor C(C), which copies the deduction candidate.

- For each deduction-guide, a function or function template with the following properties:

    - The template parameters, if any, and function parameters are those of the deduction-guide.

- (1.4.2) The return type is the simple-template-id of the deduction-guide.

Initialization and overload resolution are performed as described in 11.6 and 16.3.1.3, 16.3.1.4, or 16.3.1.7 (as appropriate for the type of initialization performed) for an object of a hypothetical class type, where the selected functions and function templates are considered to be the constructors of class type for the purpose of forming an overload set, and the initializer is provided by the context in which class template argument deduction was performed. Each nonlocal constructor is considered to be explicit if the function or function template was generated from a constructor or deduction-guide that were explicit. All such nonlocal constructors are considered to public members of the hypothetical class type.

- 3 [Example:

```cpp
template <class T> struct A {
    explicit A(const T, ...) noexcept; // #1
    A(T&, ...); // #2
};

int i;
A a1 = {i, i};

A a2(i, i); // #1 deduces to A<int> and initializes
A a3(0, i); // #2 deduces to A<int> and initializes
A a4 = {0, i}; // #2 deduces to A<int> and initializes

template <class T> A(const T, const T) -> A<T>; // #3
template <class T> explicit A(T&, T&) -> A<T>; // #4

a5 = {0, i}; // deduction guide selected in copy-list-initialization during deduction
a6(0, i); // #4 deduces to A<int> and initializes
a7 = {0, i}; // #3 deduces to A<int>, and #1 and declare same constructor
a8 = {0, i}; // #3 deduces to A<int>, and #1 and declare same constructor

template <class T> struct B {
    template <class U> B(U, T);
    template <class U> B(U, T) -> B<U>; // added for clarity
};
```

## 16.3.2 Viable functions

From the set of candidate functions (16.3.1), a set of viable functions is chosen, from which the best will be selected.

2 Initialization and overload resolution are performed as described in 11.6 and 16.3.1.3, 16.3.1.4, or 16.3.1.7 (as appropriate for the type of initialization performed) for an object of a hypothetical class type, where the selected functions and function templates are considered to be the constructors of class type for the purpose of forming an overload set, and the initializer is provided by the context in which class template argument deduction was performed. Each nonlocal constructor is considered to be explicit if the function or function template was generated from a constructor or deduction-guide that were explicit. All such nonlocal constructors are considered to public members of the hypothetical class type.

- First, to be viable, there must be enough parameters to match the arguments.

- Second, for F to be viable, there must:

1. Define ICS(F) as follows:

    - (1.1) If F is a static member function, ICS(F) is defined such that ICS(F) is neither better nor worse than ICS(G) for any function G;

    - (1.2) let the implicit conversion sequence that converts the i-th argument to the i-th parameter of F be ICS(F).

    - (1.3) If the context is an invalid user-defined conversion (see 11.6, 16.3.1.5, 16.3.1.6) and the standard conversion from the return type of F1 to the destination type (i.e., the type being initialized) is a better conversion sequence than the standard conversion sequence from the return type of F2 to the destination type;

    - (1.4) If the context is an invalid conversion function for direct reference binding (16.3.1.6) of a reference to function, the return type of F1 is the same kind of reference (i.e. lvalue) as the reference being initialized, and the return type of F2 is not.

Then, by the ranking of sequences, a viable function F is defined to be better than another viable function F if:

- For all arguments, ICS(F1) is not a worse conversion than ICS(F2), and

- For some argument j, ICS(F1) is a better conversion sequence than ICS(F2).

## 16.3.3 Best conversion sequence

Given these, a viable function F is defined to be better than another viable function F if:

- For all arguments, ICS(F1) is not a worse conversion than ICS(F2), and

- For some argument j, ICS(F1) is a better conversion sequence than ICS(F2).
