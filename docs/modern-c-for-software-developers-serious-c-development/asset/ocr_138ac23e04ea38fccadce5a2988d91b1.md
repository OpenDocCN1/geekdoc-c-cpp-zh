# Modern C++: Inline Variables (C++17)

One of the best features of C++ is its support for header-only libraries. In a header-only library, the header definitions as well as the implementation are all contained in a single header file. However, up to C++17, a header only library could not be created if the library had global variables or objects. This restriction was a consequence of the one definition rule.

According to the one definition rule (ODR), a variable or entity must be defined only once. That is, the variable must be defined in only one translation unit. Thus if a header only library defines a global variable, then this global variable will be included in all of the implementation files (.cpp) that include the single header library. In other words, we will have multiple definitions of the global variable. This is an error. For the same reason, a static member variable in a class will potentially have multiple definitions unless it is also declared as a const. The inline variable attribute in C++17 solves this problem by ensuring that a global variable in a header file is defined only once.

Beginning with C++17, we can define a global variable in a header file to be inline. Then if this header file is used in multiple translation units, the compiler will ensure that there is only one unique definition of the inline variable. The syntax for an inline variable is:

```
inline int x = 0;
class Foo {
public:
    static std::string greet = "hello world";
};
inline class Foo foo;
```