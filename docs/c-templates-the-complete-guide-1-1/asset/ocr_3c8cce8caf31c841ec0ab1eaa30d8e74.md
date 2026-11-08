```
```cpp
template<typename T> A(T) -> A<T>; // deduction guide
```
```

Without the deduction guide, we are always required (even in C++17) to specify explicit template arguments:

Click here to view code image

```
```cpp
A<int> a1(42);      // OK
A<int> a2(42);      // ERROR: not aggregate initialization
A<int> a3 = {42};   // OK
A<int> a4 = 42;     // ERROR: can't deduce type
```
```

But with the guide as written above, we can write

```
```cpp
A a = {42}; // OK
```
```

A subtlety in cases like these, however, is that the initializer must still be a valid aggregate initializer; that is, it must use a braced initializer list. The following alternatives are therefore not permitted:

Click here to view code image

```
```cpp
A a(42);  // ERROR: not aggregate initialization
A a = 42;  // ERROR: not aggregate initialization
```
```

# 15.12.2 Implicit Deduction Guides

Quite often, a deduction guide is desirable for every constructor in a class template. And the designers of class template argument deduction to include an implicit mechanism for the deduction. It is equivalent to introducing for every constructor and constructor template of the primary class template an "implicit deduction guide" as follows:

+   - The template parameter list for the implicit guide consists of the template parameters for the class template, followed by the constructor template parameters, in the template parameter list of the constructor itself.
+   - The “function-like” parameters of the guide are copied from the constructor or constructor template.
+   - The guided type of the guide is the name of the template with arguments that are the template parameters taken from the class templates.

Let's apply this on our original simple class template:

Click here to view code image

```
```cpp
template<typename T>
class A {
private:
    T t;
public:
    A(T t): t(t) {}
};
```
```

The template parameter list of the implicit guide is <typename T>, the function-like parameter list becomes just (T t), and the guided type is then A<T>. Thus, we obtain a guide that's equivalent to the user-declared guide we wrote earlier. This guide was therefore not required to achieve our desired effect. That is why, with the simple class template as originally written (and no deduction guide), we can validly write A{42}; with the expected result that t has type int.

Deduction guides have an unfortunate ambiguity. Consider again our simple class template S and the following initializations:

```
```cpp
S x(12);       // A for x type
S s = {12};    //
S y{12};       //
```
```

We already saw that s has type S<int>, but what should the type of x and y be? The two types that are intuitively are S<int> and S<int>. The committee decided somewhat controversially that it should be S<int> in both cases. Why is this controversial? Consider a similar example with a vector type:

Click here to view code image

```
```cpp
std::vector<int> v1(2, 3);  // vector<int>, not surprising
std::vector<int> v2{2, 3};  // vector<int>
std::vector v3(2, 3);       // vector<int>?
```
```

In other words, a braced initializer with one element deduces differently from a braced initialization with multiple elements. Often, the one-element scenario is what is desired, but the inconsistency is somewhat subtle. In generic code, however, it is easy to miss the subtlety:

Click here to view code image

```
```cpp
template<typename T, typename... Ts>
struct S {
    S(T t, Ts... ts);  // ... depends on pack length
};
```
```

Here is a funny fact: if T is deduced to be a vector type, the type of v will be fundamentally different depending on whether the pack is an empty or a nonempty pack.

The addition of implicit template guides themselves was not without controversy. The main argument against their inclusion is that the feature automatically adds interfaces to existing libraries. To understand this, consider once-more example close template arguments to above.