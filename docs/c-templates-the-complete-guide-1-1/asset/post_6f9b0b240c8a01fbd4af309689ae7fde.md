
```cpp
template<typename... Types>
class MyAllocator {
    Container storage; // implicitly equivalent to
    std::allocator<Types...>
};
```

```cpp
class Map {
    Container storage;
};
```

### 12.2.4 Template Parameter Packs

Since C++11, any kind of template parameter can be turned into a template parameter pack by introducing an ellipsis (...) prior to the template parameter name. If the template parameter is unnamed, where the template parameter name would occur:

```cpp
template<typename... Types> // declares a template parameter pack
class Tuple;
```

A template parameter pack behaves like its underlying template parameter, but with a crucial difference: While a normal template parameter must match exactly one template argument, a template parameter pack can match any number of template arguments. This means that the tuple class template declared above accepts any number of (possibly distinct) types as template arguments.

```cpp
template<size_t... Dimensions>
class MultiArray; // OK: declares a nontype template parameter pack

template<typename... Types>
class MultiArray; // OK: declares a type template parameter pack
```

The MultiArray example requires all nontype template arguments to be of the same type unsigned. C++17 introduced the possibility of deduced nontype template arguments, which allows us to work around that restriction to some extent—see Section 15.1.10 on page 298 for details.

For class templates, at most one template parameter pack is allowed and, if present, the template parameter pack must be the last template parameter. Function templates have a freer restriction: Multiple template parameter packs are allowed, as long as each template parameter subsequent to a template parameter pack either has a default value (see the next section) or can be deduced.

```cpp
template<typename... Types>
class ListType; // ERROR: a template parameter pack is not the last template parameter

template<typename... T>
void round(T value); // OK: by a deducible template parameter

template<typename... T, typename U>
class Tuple; // ERROR: a template parameter pack is not last
```

The last example is the declaration of a function with a deduced return type—C++14 feature. See also Section 15.10 on page 396.

Declarations of partial specializations of class and variable templates (see Chapter 16) can have multiple parameter packs, unlike their primary template counterparts. That is because partial specializations are selected through a deduction process that is nearly identical to that used for function templates.

```cpp
template<typename... Types>
class Tuple<Types...> {
    // OK: partial specialization uses deduction to
    // determine the template arguments
};
```

```cpp
template<typename T, Ts, Ta, void staticValue() {
    // ...
}
```

A template that contains a template parameter pack is called a variadic template because it accepts a variable number of template arguments. Chapter 4 and Section 12.4 on page 300 describe the use of variadic templates.

However, nested templates can create similar valid situations:

```cpp
template<typename T, struct ArgList {
    template<T> void value(T...);
};

ArgList<int, char, short> val;
```

A template that contains a template parameter pack is called a variadic template because it accepts a variable number of template arguments. Chapter 4 and Section 12.4 on page 300 describe the use of variadic templates.

### 12.2.5 Default Template Arguments

Any kind of template parameter that is not a template parameter pack can be equipped with a default argument, although it must match the corresponding parameter in kind (e.g., a type parameter cannot have a non-type default argument). A default argument cannot depend on its own parameter, because the name of the parameter is not in scope until after the default argument. However, it may depend on previous parameters:

```cpp
template<typename T, typename Allocator = allocator<T>>
class List;
```

A template parameter for a class template, variable template, or alias template can have a default template argument only if default arguments were also supplied for the subsequent parameters. (A similar constraint exists for default function call arguments.) The subsequent default values are usually provided in the template declaration, but they could also have been declared in a previous declaration of that template. The following example makes this clear:

```cpp
template<typename T1, typename T2, typename T3>
class OutputBuffer { // T4 and T5 already have defaults
};

template<typename T1, typename T2, typename T3 = char,
         typename T4 = char>
class OutputBuffer { // T4 and T5 already have defaults
};
```

Default template arguments for template parameters of function templates do not require subsequent template parameters to have a default template argument:

```cpp
template<typename T = void, typename U>
void f(); // T is not explicitly specified
```

Default template arguments cannot be repeated:

```cpp
template<typename T = void>
class Value;

template<typename T = void>
class Value; // Error: repeated default argument
```

A number of contexts do not permit default template arguments:

- Partial specializations:

    ```cpp
    template<typename T>
    class C;

    template<typename T = int>
    class C<T>; // error
    ```

- Parameter packs:

    ```cpp
    template<typename... T = int> struct X; // ERROR
    ```

- The out-of-class definition of a member of a class template:

    ```cpp
    template<typename T = int> struct X
    {
        T f();
    };

    template<typename T = int> T X<T>::f() { // ERROR
        ...
    }
    ```

```cpp
struct S {
    template<typename = void> friend struct F;
};
```

- A friend function template declaration unless it is a definition and no declaration of it appears anywhere else in the translation unit:

    ```cpp
    struct S {
        template<typename = void> friend void f() {}  // ERROR

        // A definition
        template<typename = void> friend void f();    // OK
    };
    ```

## 12.3 Template Arguments

When instantiating a template, template parameters are substituted by template arguments. The arguments can be determined using several different mechanisms:

- **Explicit template arguments:** A template name can be followed by explicit template arguments enclosed in angle brackets. The resulting name is called a *template-id*.

- **Injected class name:** Within the scope of a class template `X` with template parameters `P1`, `P2`, ..., the name of that template (`X`) can be equivalent to the template-id `X<P1, P2, ...>`.

- **Default template arguments:** Explicit template arguments can be omitted from template instances if default template arguments are available. However, for a class or alias template, even if all template parameters have a default value, the (possibly empty) angle brackets must be provided.

- **Argument deduction:** Function template arguments that are not explicitly specified may be deduced from the types of the function call arguments. In a call this is described in detail in Chapter 15. Deduction is also done in a few other situations. If all the template arguments can be deduced, no angle brackets need to be specified after the name of the function template. C++17 also introduces the ability to deduce class template arguments from the initializer of a variable declaration or functional-notation type conversion; see Section 15.2 on page 73 for a discussion.

### 12.3.1 Function Template Arguments

Template arguments for a function template can be specified explicitly, deduced from the way the template is used, or provided as a default template argument. For example:

`detail/max.cpp`

```cpp
template<typename T>
T max (T a, T b)
{
    return b < a ? a : b;
}

int main()
{
    auto x = max<double>(1.0, -3.0);   // explicitly specify each
    auto y = max(1.0, -3.0);           // template argument is deduced
    auto z = max<int>(1.0, 2.0);       // explicit template argument
                                       // hence the result has type int
}
```

Some template arguments can never be deduced because their corresponding template parameter does not appear in a function parameter type or for some other reason (see Section 15.2 on page 73). The corresponding parameters are typically placed at the beginning of the list of template arguments so they can be specified explicitly while all other arguments are to be deduced. For example:

`detail/implicit.cpp`

```cpp
template<typename DestT, typename SrcT>
DestT implicit_cast(SrcT const& x)  // SrcT can be deduced
{
```
