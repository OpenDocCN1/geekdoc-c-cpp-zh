member data). Superficially, abstract classes and interfaces are similar. C++ does not support interfaces; however, we can emulate them by creating (variadic) tuples whose elements are universal function wrappers. In this case we define our interface emulator as:

```
template <typename T>
    using ISde = std::tuple<FunctionType<T>, FunctionType<T>>;
```

We create an instance of ISde as follows, for example:

```
auto drift = [=](T t, T S) { return mu; };
auto diffusion = [=](T t, T S) { return sig; };
```

```
ISde<T> functions = std::make_tuple(drift, diffusion);
```

We then use functions in a constructor of Sde<> as already discussed. Another way to emulate interfaces is to create a struct that is composed of one or more universal function wrappers.

# 6.10 SUMMARY AND CONCLUSIONS

In this chapter we introduced several advanced language features in C++ that can be used when creating generic libraries, generic lambda functions and when moving to multiparadigm design methods. We also show how to define *higher-order functions* that can be used in numerical analysis and computational finance. We shall extend these functional programming features in later chapters.

In Section 6.9 we included a summary of the essential features of what a multiprogramming design approach entails in the context of classes that model stochastic differential equations. A relevant set of questions is given in Exercise 12, in which we discuss design issues from a number of viewpoints.

# 6.11 EXERCISES AND PROJECTS

+   1. Give the top two advantages of *type traits*:
+      a) Creating type-independent code.
+      b) ‘Compile-time’ *reflection*.
+      c) It is a replacement for subtype polymorphism.
+      d) It is used to add properties to C++ types.
+   
+   2. Consider the code:

```
// Testing arithmetic types
std::cout << "int*: " << std::boolalpha << std::is_arithmetic<int*>::value;

std::cout << "std::complex<double>: " << std::boolalpha
          << std::is_arithmetic<std::complex<double>>::value;

std::cout << "char: " << std::boolalpha << std::is_arithmetic<char>::value;
```