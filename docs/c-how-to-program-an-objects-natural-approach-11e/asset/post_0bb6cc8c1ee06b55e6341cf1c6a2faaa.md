
There are two types of metafunctions:

- A **value metafunction** is a class template with a **public static constexpr data member typically named value**. The class template uses its template arguments to compute a value at compile time. This is how we implement factorial calculations.
- A **type metafunction** is a class template with a **nested type member**, typically defined as a **type alias**. The class template uses its template arguments to manipulate a type at compile time. Section 15.13.4 presents type metafunctions.

The metafunction member names value and type are conventions⁹⁸ used throughout the C++ standard library and in metaprogramming in general.

### Factorial Metafunction

Our Factorial metafunction (lines 6–9) is implemented using the recursive factorial definition

$$n! = n \cdot (n - 1)!$$

Factorial has **one non-type template parameter**—the int parameter N (line 6)—representing the metafunction’s argument. Per the C++ standard’s conventions for value metafunctions, line 8 defines a public static constexpr data member named value. Factorials grow quickly, so we declared the variable’s type as long long. The constant value is initialized with the result of the expression `N * Factorial<N - 1>::value`, which multiplies N by the result of “calling” the Factorial metafunction for N - 1.

### “Calling” a Metafunction

You **“call” a metafunction by instantiating its template**, which probably feels weird to you. For example, to calculate the factorial of 3, you’d use

`Factorial<3>::value`

in which 3 is the template argument and `::value` is the **“return value.”** This expression causes the compiler to create a new type representing the factorial of 3. We’ll say more about this momentarily.

### Factorial Metafunction Specialization for the Base Case—`Factorial<0>`

For the recursive factorial calculation, 0! is the base case, which is defined to be 1. In metafunction recursion, you specify the base case with a full template specialization (lines 12–15). Such a specialization uses the notation `template <>` (line 12) to indicate that all the template’s arguments will be specified explicitly in the angle brackets following the class name. The full template specialization `Factorial<0>` matches only Factorial calls with the argument 0. Line 14 sets the specialization’s value member to be 1.⁹⁹

### How the Compiler Evaluates Metafunction Factorial for the Argument 0

When the compiler encounters a metafunction call, such as `Factorial<0>::value` (line 43 in main), it must determine which `Factorial` class template to use. The template argument is the int value 0. The class template `Factorial` in lines 6–9 can match any int value. The full-template specialization `Factorial<0>` in lines 12–15 specifically matches only the value 0. **The compiler always chooses the most specialized template from multiple matching templates.** So, `Factorial<0>` matches the full template specialization, and `Factorial<0>::value` evaluates to 1.

### How the Compiler Evaluates Metafunction Factorial for the Argument 3

Now, let’s reconsider the metafunction call `Factorial<3>::value` (line 46 in main). The compiler generates each specialization needed to produce the final result at compile-time. When the compiler encounters `Factorial<3>::value`, it specializes the class template in lines 6–9 with 3 as the argument. In doing so, line 8 of the specialization becomes

`3 * Factorial<2>::value`

The compiler sees that to complete the `Factorial<3>` definition, it must specialize the template again for `Factorial<2>`. In that specialization, line 8 becomes

`2 * Factorial<1>::value`

Next, the compiler sees that to complete the `Factorial<2>` definition, it must specialize the template again for `Factorial<1>`. In that specialization, line 8 becomes

`1 * Factorial<0>::value`

The compiler knows that `Factorial<0>::value` is 1 from the full specialization in lines 12–15. This completes the `Factorial` specializations for `Factorial<3>`.

Now, the compiler knows everything it needs to complete the earlier `Factorial` specializations:

- `Factorial<1>::value` stores the result of 1 * 1, which is 1.
- `Factorial<2>::value` stores the result of 2 * 1, which is 2.
- `Factorial<3>::value` stores the result of 3 * 2, which is 6.

So the compiler can insert the final constant value 6 in place of the original metafunction call—**without any runtime overhead.** Each of the `Factorial` metafunction calls in lines 43–48 of main are evaluated similarly by the compiler, **enabling it to perform these calculations at compile-time.**

### Functional Programming

None of what the compiler does during **template specialization** modifies variable values after they’re initialized.¹⁰⁰ **There are no mutable variables in template metaprograms**—this is a hallmark of **functional programming.** All the values processed in this example are compile-time constants.

### Using `constexpr` Functions to Perform Compile-Time Calculations

As you can see, using metafunctions to calculate values at compile-time is more complex than using traditional runtime functions. C++ provides two options for compile-time evaluation of traditional functions:

- A function declared `constexpr` can be called at compile-time or runtime.
- In C++20, you can declare a function `consteval` (rather than `constexpr`) to indicate that it can be called only at compile-time to produce a constant.

Many computations performed with metafunctions are easier to implement using traditional functions that are declared `constexpr` or `consteval`. Such functions also are part of compile-time metaprogramming. In fact, various members of the C++ standard committee prefer constexpr-based metaprogramming over template-based metaprogramming, which is “difficult to use, does not scale well and is basically equivalent to inventing a new language within C++.”¹⁰¹ They’ve proposed various constexpr enhancements to simplify other aspects of metaprogramming in future C++ versions.

Lines 18–25 and 28–36 define the `recursiveFactorial` and `iterativeFactorial` functions using the algorithms from Section 5.16 and traditional C++ syntax. Each function is declared constexpr, so the compiler can evaluate the function’s result at compile-time. Lines 53–58 demonstrate `recursiveFactorial`, and lines 63–68 demonstrate `iterativeFactorial`.

## 15.13.3 Conditional Compilation with Template Metaprogramming and `constexpr if`

Another aspect of doing more at compile-time to optimize runtime execution is generating code that executes optimally at runtime. Section 15.6.4 showed the C++20 way to optimize runtime execution for a `customDistance` function template using concept-based function overloading. In that example, the compiler chose the correct overloaded function template to call based on the template parameter’s type constraints. Figure 15.20 reimplements that example using a single `customDistance` function template, showing how you could implement similar functionality before concepts. Inside the function, we use a compile-time if statement—`constexpr if`—with `std::is_base_of_v` (the shorthand for accessing type trait `std::is_base_of`’s value member) to decide whether to generate the `O(1)` or `O(n)` distance calculation based on whether the function’s iterator arguments are

- random-access iterators (or the derived iterator category contiguous iterators) that can be used to perform an `O(1)` distance calculation or
- lesser iterators for which we’ll perform the `O(n)` distance calculation.

```cpp
// fig15_20.cpp
// Implementing customDistance using template metaprogramming.
#include <array>
#include <iterator>
```

**Fig. 15.20**  |  Implementing customDistance using template metaprogramming. (Part 1 of 2.)

98. Jody Hagins, “Template Metaprogramming: Type Traits (Part 1 of 2),” YouTube video, September 22, 2020. Accessed April 18, 2023. https://www.youtube.com/watch?v=tiAWcjTf6o.
99. Section 5.16 specified that 0 and 1 are both base cases for factorial calculations. To mimic that, we could implement a second full template specialization named `Factorial<1>`. As implemented, the Factorial metafunction handles `Factorial<1>` as `1 * Factorial<0>`.
100. “Template Metaprogramming.” Wikipedia.
101. Louis Dionne, “Metaprogramming by Design, Not By Accident,” June 18, 2017. Accessed April 18, 2023. https://wg21.link/p0425r0.
