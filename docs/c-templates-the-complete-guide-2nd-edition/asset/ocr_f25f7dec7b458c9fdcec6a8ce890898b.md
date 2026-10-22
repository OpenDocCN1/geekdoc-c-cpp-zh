```
```cpp
{
undeclared(); // first-phase compile-time error if undeclared()
unknown
undeclared(t); // second-phase compile-time error if undeclared(T)
unknown
static_assert(sizeof(int) > 10, // always fails if sizeof(int)<=10
"int too small");
static_assert(sizeof(T) > 10, //fails if instantiated for T with size
<=10
"T too small");
}
```
```

The fact that names are checked twice is called *two-phase lookup* and discussed in detail in Section 14.3.1 on page 249.

Note that some compilers don’t perform the full checks of the first phase.⁶ So you might not see general problems until the template code is instantiated at least once.

# Compiling and Linking

Two-phase translation leads to an important problem in the handling of templates in practice: When a function template is used in a way that triggers its instantiation, a compiler will (at some point) need to see that template’s definition. This breaks the usual compile and link distinction for ordinary functions, when the declaration of a function is sufficient to compile its use. Methods of handling this problem are discussed in Chapter 9. For the moment, let’s take the simplest approach: Implement each template inside a header file.

# 1.2 Template Argument Deduction

When we call a function template such as `max()` for some arguments, the template parameters are determined by the arguments we pass. If we pass two `ints` to the parameter types T, the C++ compiler has to conclude that T must be `int`.

However, T might only be “part” of the type. For example, if we declare `max()` to use constant references: [Click here to view code image](#)

```
```cpp
template<typename T>
T max (T const& a, T const& b)
{
return b < a ? a : b;
}
```
```