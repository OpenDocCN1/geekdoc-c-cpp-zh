Lines 33–34 define an array and a list. Line 36 calls `customDistance` for the array `ints1`, which has random-access iterators. Our function that requires input iterators could receive random-access iterators. However, when multiple function templates satisfy a function call, the compiler calls the most constrained version. So line 36 calls the `O(1)` version of `customDistance` (lines 26–30). Based on their definitions, the compiler knows that `random_access_iterator` is more constrained than `input_iterator`. For the call in line 38, a list’s bidirectional iterators do not satisfy the constraints of the function template in lines 26–30. So, that version is eliminated from consideration, and the slower `O(n)` customDistance in lines 11–22 is called.

# 15.6.5 requires Expressions

The C++ Core Guidelines recommend using standard concepts. For custom requirements that cannot be expressed via standard concepts in a `requires` clause, you can use a requires expression, which has two forms:

```
requires {
  requirement-definitions
}

or

requires (parameter-list) {
  requirements-definitions that optionally use the parameters
}
```

The parameter-list looks like a function’s parameter list but cannot have default arguments. The compiler uses a requires expression’s parameters only to check whether types satisfy the requirements defined in the expression’s braces. The braces may contain any combination of the four requirement types described below—simple, type, compound and nested. Each requirement ends with a semicolon (;).

# Simple Requirements

A simple requirement checks whether an expression is valid. Consider the definition of the `<ranges>` header’s range concept, which checks whether an object’s type represents a C++20 range with a begin iterator and an end sentinel:

```
template<class T>
concept range =
  requires(T& t) {
    std::ranges::begin(t);
    std::ranges::end(t);
  };
```

53. Hendrik Niemeyer, “An Introduction to C++20’s Concepts,” July 25, 2020. Accessed April 18, 2023. https://www.youtube.com/watch?v=N_kPd20KlI8.

54. C++ Standard, “13.5 Template Constraints.” Accessed April 18, 2023. https://timsong-cpp.github.io/cppwp/n4861/temp.constr.

55. C++ Core Guidelines, “T.11: Whenever Possible Use Standard Concepts.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#rst-std-concepts.

56. C++ Standard, “24.4.2 Ranges.” Accessed April 18, 2023. https://timsong-cpp.github.io/cppwp/n4861/ranges#range.