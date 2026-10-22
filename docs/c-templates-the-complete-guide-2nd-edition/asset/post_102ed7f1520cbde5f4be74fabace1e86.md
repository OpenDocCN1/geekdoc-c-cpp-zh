
```cpp
{
    undeclared(); // first-phase compile-time error if undeclared()
    undeclared(t); // second-phase compile-time error if undeclared(T)
    static_assert(sizeof(int) > 10, // always fails if sizeof(int)<=10
                  "int too small");
    static_assert(sizeof(T) > 10, // fails if instantiated for T with size <=10
                  "T too small");
}
```

The fact that names are checked twice is called *two-phase lookup* and discussed in detail in Section 14.3.1 on page 249.

Note that some compilers don’t perform the full checks of the first phase.⁶ So you might not see general problems until the template code is instantiated at least once.

### Compiling and Linking

Two-phase translation leads to an important problem in the handling of templates in practice: When a function template is used in a way that triggers its instantiation, a compiler will (at some point) need to see that template’s definition. This breaks the usual compile and link distinction for ordinary functions, when the declaration of a function is sufficient to compile its use. Methods of handling this problem are discussed in Chapter 9. For the moment, let’s take the simplest approach: Implement each template inside a header file.

## 1.2 Template Argument Deduction

When we call a function template such as `max()` for some arguments, the template parameters are determined by the arguments we pass. If we pass two `ints` to the parameter type T, the C++ compiler has to conclude that T must be `int`.

However, T might only be “part” of the type. For example, if we declare `max()` to use constant references:

```cpp
template<typename T>
T max (T const& a, T const& b)
{
    return b < a ? a : b;
}
```

and pass int, again T is deduced as int, because the function parameters match for `int const&`.

### Type Conversions During Type Deduction

Note that automatic type conversions are limited during type deduction:

- When declaring call parameters by reference, even trivial conversions do not apply to type deduction. Two arguments declared with the same template parameter `T` must match exactly.
- When declaring call parameters by value, only trivial conversions that decay are supported: qualifiers with `const` or `volatile` are ignored, references convert to the referenced type, and raw arrays or functions convert to the corresponding pointer type. For two arguments declared with the same template parameter `T` the decayed types must match.

For example:

```cpp
template<typename T>
T max (T a, T b);
...
int const c = 42;
max(i, c); // OK: T is deduced as int
max(c, c); // OK: T is deduced as int
int& ir = i;
max(i, ir); // OK: T is deduced as int
int arr[4];
foo(&i, arr); // OK: T is deduced as int*
```

However, the following are errors:

```cpp
max(4, 7.2); // ERROR: T can be deduced as int or double
std::string s;
foo("hello", s); // ERROR: T can be deduced as char const[6] or std::string
```

There are three ways to handle such errors:

1. Cast the arguments so that they both match:

   ```cpp
   max(static_cast<double>(4), 7.2); // OK
   ```

2. Specify (or qualify) explicitly the type of `T` to prevent the compiler from attempting type deduction:

   ```cpp
   max<double>(4, 7.2); // OK
   ```

3. Specify that the parameters may have different types.

Section 1.3 on page 9 will elaborate on these options. Section 7.2 on page 108 and Chapter 15 will discuss the rules for type conversions during type deduction in detail.

### Type Deduction for Default Arguments

Note also that type deduction does not work for default call arguments. For example:

```cpp
template<typename T>
void f(T = "");
...
```

```cpp
f(1); // OK: deduced T to be int, so that it calls f<int>(1)
f(); // ERROR: cannot deduce T
```

To support this case, you also have to declare a default argument for the template parameter, which will be discussed in Section 1.4 on page 13:

```cpp
template<typename T = std::string>
void f(T = "");

f(); // OK
```

## 1.3 Multiple Template Parameters

As we have seen so far, function templates have two distinct sets of parameters:

1. Template parameters, which are declared in angle brackets before the function template name:

   ```cpp
   template<typename T> // T is template parameter
   ```

2. Call parameters, which are declared in parentheses after the function template name:

   ```cpp
   T max (T a, T b) // a and b are call parameters
   ```

You may have as many template parameters as you like. For example, you could define the `max()` template for call parameters of two potentially different types:

```cpp
template<typename T1, typename T2>
T1 max (T1 a, T2 b)
{
    return b < a ? a : b;
}
...
auto m = ::max(4, 7.2); // OK, but type of first argument defines return type
```

It may appear desirable to be able to pass parameters of different types to the `max()` template, but, as this example shows, it raises a problem. If you use one of the parameter types as return type, the argument for the other parameter might get converted to this type, regardless of the caller’s intention. Thus, the return type depends on the call argument order. The maximum of 66.66 and 42 will be the `double` 66.66, while the maximum of 42 and 66.66 will be the `int` 66.

- Introduce a third template parameter for the return type.
- Let the compiler find out the return type.
- Declare the return type to be the “common type” of the two parameter types.

All these options are discussed next.

### 1.3.1 Template Parameters for Return Types

Our earlier discussion showed that *template argument deduction* allows us to call function templates with syntax identical to that of calling an ordinary function: We do not have to explicitly specify the types corresponding to the template parameters.

We also mentioned, however, that we can specify the types to use for the template parameters explicitly:

```cpp
template<typename T>
T max (T a, T b);
...
::max<double>(4, 7.2); // instantiate T as double
```

In cases when there is no connection between template and call parameters and when template parameters cannot be determined, you must specify the template argument explicitly with the call. For example, you can introduce a third template argument type to define the return type of a function template:

```cpp
template<typename T1, typename T2, typename RT>
RT max (T1 a, T2 b);
```

```cpp
template<typename T1, typename T2>
auto max (T1 a, T2 b)
{
    return b < a ? a : b;
}
```

In fact, the use of `auto` for the return type without a corresponding *trailing return type* (which would be introduced with a `->` at the end) indicates that the actual return type must be deduced from the return statements in the function body. Of course, deducing the return type from the function body has to be possible. Therefore, the code must be available and multiple return statements have to match.

Before C++14, it is only possible to let the compiler determine the return type by more or less making the implementation of the function part of its declaration. In C++11 we can benefit from the fact that the *trailing return type* syntax allows us to use the call parameters. That is, we can declare that the return type is derived from what `operator?:` yields:

```cpp
template<typename T1, typename T2>
auto max (T1 a, T2 b) -> decltype(b<a?a:b)
{
    return b < a ? a : b;
}
```

Here, the resulting type is determined by the rules for `operator?:`, which are fairly elaborate but generally produce an intuitively expected result (e.g., if a and b have different arithmetic types, a common arithmetic type is found for the result).

Note that

```cpp
template<typename T1, typename T2>
auto max (T1 a, T2 b) -> decltype(b<a?a:b);
```

is a declaration, so that the compiler uses the rules of `operator?:` called for parameters a and b to find out the return type of `max()` at compile time. The implementation does not necessarily have to match. In fact, using `true` as the condition for `operator?:` in the declaration is enough:

```cpp
template<typename T1, typename T2>
```
