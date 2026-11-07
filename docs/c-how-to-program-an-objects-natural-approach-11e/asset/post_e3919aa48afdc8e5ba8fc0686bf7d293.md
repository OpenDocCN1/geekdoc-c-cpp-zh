
template. As you’ll see, you’ll also receive error messages that generally are easier to understand.

## 15.3.2 C++20 Templated Lambdas

In C++20, lambdas can specify template parameters. Consider the following lambda from Fig. 14.16, which we used to calculate the sum of the squares of an array’s integers:

```
[](auto total, auto value) {return total + value * value;}
```

The compiler independently infers total’s and value’s (possibly different) types from their arguments. **You can force the lambda to require the same type for both** by using a templated lambda:

```
[]<typename T>(T total, T value) {return total + value * value;}
```

The template parameter list is placed between the lambda’s introducer and parameter list. **When you use one type parameter (T) to declare both lambda parameters, the compiler requires both arguments to have the same type;** otherwise, a compilation error occurs.

## 15.4 C++20 Concepts: A First Look

**Concepts** (briefly introduced in Section 14.2) simplify generic programming. C++ experts say that “Concepts are a revolutionary approach for writing templates”²⁰ and that “C++20 creates a paradigm shift in the way we use metaprogramming.”²¹ C++’s creator, Bjarne Stroustrup, says, “Concepts complete C++ templates as originally envisioned” and that they’ll “dramatically improve your generic programming and make the current work-arounds (e.g., traits classes) and low-level techniques (e.g., enable_if-based overloading) feel like error-prone and tedious assembly programming.”²²

As you’ll see, concepts constrain the arguments specified for a template’s parameters. You’ll use **requires clauses** and **requires expressions** to specify constraints, which can

- **test attributes of types** (e.g., “Is the type an integer type?”) and
- **test whether types support various operations** (e.g., “Does a type support the comparison operations?”).

The C++ standard provides 74 **predefined concepts** (see Section 15.4.3), and you can create custom concepts. Each defines a type’s requirements or a relationship between types.²³ **Concepts can be applied to any template parameter and to any use of auto.**²⁴ We’ll discuss concepts in more depth in Section 15.6. Initially, we’ll focus on using concepts to constrain a function template’s type parameters.

### Motivation and Goals of Concepts

Stroustrup says, “Concepts enable overloading and eliminate the need for a lot of ad-hoc metaprogramming and much metaprogramming scaffolding code, thus significantly simplifying metaprogramming as well as generic programming.”²⁵

Traditionally, **template requirements were implicit**, based on how the template used its arguments in operator expressions, function calls, etc.²⁶ This was the case in Fig. 15.3’s abbreviated function template `printContainer`. The function definition did not indicate that the argument must be iterable with the range-based for statement or that the element type must support the `<<` operator for output. Though such requirements typically would be documented in program comments, **the compiler cannot enforce comments**. To determine that a type was incompatible with a template, the compiler first had to attempt to instantiate the template to “see” that a type did not support the template’s implicit requirements. This led to many, often cryptic, compilation errors.

**Concepts specify template requirements explicitly in code. They enable the compiler to determine that a type is incompatible with a template before instantiating it**—leading to fewer, more precise error messages and potential compile-time performance improvements.²⁷

**Concepts also enable you to overload function templates with the same signature based on each function template’s requirements.**²⁸ For example, we’ll define two different overloads of a function template with the same signature:

- one will **support any container with input iterators** and
- the other will be **optimized for containers with random-access iterators**.

### 15.4.1 Unconstrained Function Template `multiply`

When you call a function, the compiler uses its **overload-resolution rules**²⁹ and a technique called **argument-dependent lookup (ADL)**³⁰,³¹,³²,³³ to locate all the function definitions that might satisfy the function call. Together, these are known as the overload set. This process often includes instantiating function templates based on a function call’s argument types. The compiler then chooses the best match from the overload set. **An unconstrained function template does not explicitly specify any requirements.** So the compiler substitutes the call’s argument types into the function template’s declaration to check whether it is a viable match and, if so, whether it is the best match. If it’s the best match, the compiler will instantiate the template’s definition and determine whether the argument types support the operations used in the function template’s body.

Consider the **unconstrained function template** `multiply` (lines 5–6 of Fig. 15.4), which receives **two values of the same type** (T) and returns their product.

```cpp
// fig15_04.cpp
// Simple unconstrained multiply function template.
#include <iostream>

template<typename T>
T multiply(T first, T second) {return first * second;}

int main() {
    std::cout << "Product of 5 and 3: " << multiply(5, 3)
              << "\nProduct of 7.25 and 2.0: " << multiply(7.25, 2.0) << "\n";
}
```

```
Product of 5 and 3: 15
Product of 7.25 and 2.0: 14.5
```

**Fig. 15.4** | Simple unconstrained multiply function template.

This template has **implicit requirements** that you can infer from the code:

- The parameter types (line 6) are not pointers or references, so the **arguments are received by value**. Similarly, the return type is not a pointer or a reference, so the result is returned by value. Thus, **the arguments’ type must support copying or moving**.
- The arguments are multiplied, so **the arguments’ type must support the binary `*` operator**, either natively (as with built-in types like int and double) or via operator overloading.

When the compiler instantiates `multiply` for a given type and determines that the arguments are incompatible with the template’s implicit requirements, **it eliminates the function from the overload set**. In this example, lines 9 and 10 call `multiply` with two int values and two double values, respectively. **All numeric types in C++ support this template’s implicit requirements**, so the compiler can instantiate `multiply` for each type. Interestingly, **you cannot call `multiply` with arguments of different types**, even if one argument’s type can be implicitly converted to the other’s. There’s one type parameter, so both arguments must have identical types.

### Using Incompatible Types with `multiply`

What if we pass to `multiply` arguments that **do not support** the template’s implicit requirements and there is no other function declaration that better matches the function call? The compiler will generate error messages. For example, the following code attempts to calculate the product of two strings.³⁴

**Footnotes**

20. Bartlomiej Filipek, “C++20 Concepts—A Quick Introduction,” May 5, 2021. Accessed April 18, 2023. https://www.cppstories.com/2021/concepts-intro/.
21. Inbal Levi, “Exploration of C++20 Metaprogramming,” September 29, 2020. Accessed April 18, 2023. https://www.youtube.com/watch?v=XgrjybKaIW8.
22. Bjarne Stroustrup, “Concepts: The Future of Generic Programming—3.1 Specifying Template Interfaces,” January 31, 2017. Accessed April 18, 2023. http://wg21.link/p0557r0.
23. Bjarne Stroustrup, “Concepts: The Future of Generic Programming—3.1 Specifying Template Interfaces,” January 31, 2017. Accessed April 18, 2023. http://wg21.link/p0557r0.
24. “Placeholder Type Specifiers.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/language/auto.
25. Bjarne Stroustrup, “Concepts: The Future of Generic Programming—3 Using Concepts,” January 31, 2017. Accessed April 18, 2023. https://wg21.link/p0557r0.
26. Hendrik Niemeyer, “An Introduction to C++20’s Concepts,” July 25, 2020. Accessed April 18, 2023. https://www.youtube.com/watch?v=N_kPd20K1L8.
27. The error messages’ quality and quantity still vary considerably among compilers.
28. This enables even a class’s no-argument constructor to be overloaded with specific constraints.
29. “Overload Resolution.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/language/overload_resolution.
30. C++ Standard, “6.5.4 Argument-Dependent Name Lookup [basic.lookup.argdep].” Accessed April 18, 2023. https://timsong-cpp.github.io/cppwp/n4861/basic.lookup.argdep#:~:text=lookup,argument-dependent.
31. “Argument-Dependent Lookup.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/language/adl.
32. Inbal Levi, “Exploration of C++20 Metaprogramming,” September 29, 2020. Accessed April 18, 2023. https://www.youtube.com/watch?v=XgrjybKaIW8.
33. Arthur O’Dwyer, “What Is ADL?” April 26, 2019. Accessed April 18, 2023. https://quuxplusone.github.io/blog/2019/04/26/what-is-adl/.
34. For your convenience, this code is provided in the source-code file as comments at the end of main.
