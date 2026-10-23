
member data). Superficially, abstract classes and interfaces are similar. C++ does not support interfaces; however, we can emulate them by creating (variadic) tuples whose elements are universal function wrappers. In this case we define our interface emulator as:

```cpp
template <typename T>
    using ISde = std::tuple<FunctionType<T>, FunctionType<T>>;
```

We create an instance of ISde as follows, for example:

```cpp
auto drift = [=](T t, T S) { return mu; };
auto diffusion = [=](T t, T S) { return sig; };

ISde<T> functions = std::make_tuple(drift, diffusion);
```

We then use functions in a constructor of Sde<> as already discussed. Another way to emulate interfaces is to create a struct that is composed of one or more universal function wrappers.

## 6.10 SUMMARY AND CONCLUSIONS

In this chapter we introduced several advanced language features in C++ that can be used when creating generic libraries, generic lambda functions and when moving to multiparadigm design methods. We also show how to define *higher-order functions* that can be used in numerical analysis and computational finance. We shall extend these functional programming features in later chapters.

In Section 6.9 we included a summary of the essential features of what a multiparadigm design approach entails in the context of classes that model stochastic differential equations. A relevant set of questions is given in Exercise 12, in which we discuss design issues from a number of viewpoints.

## 6.11 EXERCISES AND PROJECTS

### 1. Give the top two advantages of *type traits*:

a) Creating type-independent code.
b) 'Compile-time' *reflection*.
c) It is a replacement for subtype polymorphism.
d) It is used to add properties to C++ types.

### 2. Consider the code:

```cpp
// Testing arithmetic types
std::cout << "int*: " << std::boolalpha << std::is_arithmetic<int*>::value;

std::cout << "std::complex<double>: " << std::boolalpha
          << std::is_arithmetic<std::complex<double>>::value;

std::cout << "char: " << std::boolalpha << std::is_arithmetic<char>::value;

std::cout << "std::bitset<8>: " << std::boolalpha
          << std::is_arithmetic<std::bitset<8>>::value;
```

Which option is the correct output?

a) false, false, false, false.
b) false, false, true, false.
c) false, true, false, true.
d) false, true, true, true.

### 3. (Arithmetic Types)

a) Which of the following types are of arithmetic type? `int`, `int const`, `int &`, `int *`, `float`, `float const`, `float &`, `float *`.
b) Consider `std::complex<double>`. Does it fit into the following composite type categories? `is_{fundamental, arithmetic, scalar, object, compound}`.
c) In which composite type categories does `std::array<>` fit? Is it a non-union class type?

### 4. Which statements describe a variadic function?

a) Arguments whose types are variant.
b) Takes a variable number of template arguments.
c) Takes a variable number of arguments of specific types.
d) C++11 does not support variadic functions; they are supported in C++14.

### 5. Which of the following statements are true regarding a variadic function?

a) It is declared using ellipses.
b) It is not possible to make a copy of the variadic function arguments.
c) It accepts any number of arguments.
d) A template with at least one parameter pack is called a variadic template.

### 6. (Other Type Traits, Investigation)

This exercise entails determining which type traits functions to use for the following functionality. Having discovered the appropriate functions then create some code with two specific types to show how it works:

a) Is a type either a signed or an unsigned arithmetic type?
b) Make a given integral type signed/unsigned.
c) Obtain the number of dimensions of an array type.
d) Remove/add a pointer from or to a given type.
e) Remove/add a reference from or to a given type.

### 7. (Pointers and Non-pointers)

This exercise consists of calling some functions from the Primary type category.
Answer the following questions:

a) Write a function to determine if a type is a pointer, null pointer, lvalue reference or rvalue reference.
b) Determine if a type is a member function pointer or if it is a pointer to a non-static member object.
c) Is a shared pointer a pointer type? Is it a pointer type when converted to a raw pointer? Typical code is:

```cpp
template <typename T>
    void IsPointer(const T& t)
{ // First example of type_traits; check if t is a pointer
    // Return type is std::true_type or std::false_type
    if (std::is_pointer<T>::value)
    {
        std::cout << "This is a pointer type argument\n";
    }
    else
    {
        std::cout << "not a pointer type argument\n";
    }
}
```

### 8. (Simple Switchable Bridge Functionality)

We create a template function that supports both pointers and reference types. If it is a pointer it is dereferenced and then printed while if it is not a pointer type and if it is a scalar/reference type then it is printed directly. Use this is_pointer() function in conjunction with std::true_type and std::false_type to determine which implementation to call.

### 9. (Array Categories)

We discuss some functions that work with array types. The *rank* of an array type is equal to the number of dimensions of the array. The *extent* of an array type is the number of elements along the Nth dimension of the array if N is in the closed interval [0, std::rank<T>::value]. For any other type, the value is 0.

Answer the following questions:

a) Test `std::is_array()` on a range of fundamental, scalar, object, arithmetic and compound types.

b) Create an array `int [][3][4][5]`. Find its rank and extent.

c) Call `std::remove_extent()` and `std::remove_all_extents()` on the array in question b). What is happening?

### 10. (Conversions)

Sometimes you may wish to structurally change fundamental properties of types in an application. Examples are:

- Mapping integers to unsigned integers and vice versa.
- Adding/removing the const specifier to or from a type.
- Adding/removing a pointer to or from a type.
- Adding/removing the volatile specifier to or from a type.

Answer the following questions:

a) Write a separate function for each of the above requirements.

b) Test the functions on a range of fundamental, scalar, object, arithmetic and compound types.

### 11. (Capture Modes, Brainstorming Question)

In Sections 6.5, 6.6 and 6.7 we introduced generic lambda functions, some examples and how to deal with captured variables. It is natural to ask which solution is most appropriate in a given context. We have given code examples in this chapter to help you answer the following questions. Of course, a definitive answer can only be given when you actually develop your own applications and make your own conclusions:

a) Compare generic lambdas and template functions with regard to reliability, maintainability and understandability.

b) We can capture by value, by reference, by generalised capture, by local variables and by emulation using std::bind. Give the two best candidates from this list that satisfy the following requirements: maintainability, efficiency, understandability and interoperability with client code.

c) How do the techniques in part b) scale to larger and more complex code blocks? In which sense are encapsulation and information hiding potentially compromised (if at all) by the introduction of captured variables?

d) As a follow-on to question c), in which circumstances would we prefer to use function objects instead of the other techniques? Would they improve maintainability or efficiency?

e) Is there a need to emulate generalised lambda capture using C++11 and std::bind? Are there potential benefits?

f) How would you reimplement the code in Section 6.7.1 using a function object? Would it be a better solution?

### 12. (Creating Stochastic Differential Equations, Brainstorming)

The approach in Section 6.9 seems to be relatively new and innovative. We have asked several quant developers for their opinions on how useful it is as a competitor to their current design style.

We reproduce the answer from one user:

Question: Is this approach to polymorphism 'better' than e.g. subtype polymorphism?

Answer: I would say that the benefit of this kind of scheme is that there is only one class (OneFactorProcess) instead of one base class (which is nothing more than an abstract interface) and several implementation classes. The drift and diffusion coefficients can be built outside the OneFactorProcess class. I see that by using this scheme we can increase flexibility on how the actual SDE (drift and diffusion coefficients) will be built. I think this is one of the strongest arguments for using this kind of scheme. Finally, it feels like a modern way to do things – at least for myself.

Incidentally, we use the alias:

```cpp
template <typename T>
    using OneFactorProcess = Sde<T>;
```

Question: Does this approach lead to more maintainable code?

Answer: I would say yes.

Question: Does the approach scale to larger systems?

Answer: Well, if you consider my own path generator as a larger system, then yes. I see no reason why this scheme would not be implementable for any system, despite its complexity, as long as all interfaces between components are well designed.
