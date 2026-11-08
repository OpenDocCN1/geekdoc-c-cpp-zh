
```cpp
auto b = Direction<int, Ratio<2, 3>>{y};   // 2 / 3 seconds
auto c = a + b;   // computes resulting unit type 1/3000 seconds

b * 1200;   // and generates run-time code for c = a * 3 seconds
```

The key “hybrid” effect is that the same type compiler determines the resulting unit type `Ratio<1, 3000>` at compile time and generates code to compute at run time the resulting value, which is adjusted for the resulting unit type.

Because the value type is a template parameter, we can use class Duration with value types other than int, or even use heterogeneous value types (as long as adding the values of those types is defined):

[Click here to view code image](#)

```cpp
auto d = Duration<double, Ratio<3, 1>>{1.5};   // 3 / 1 seconds
auto e = Duration<int, Ratio<1, 1>>{2};         // 1 / 1 seconds
auto f = d + e;   // computes resulting unit type 1/3 sec
                  // and generates code for d + e * 3
```

In addition, the compiler can even perform the value computation at compile time if the values are known at compile time, because constexpr is a C++ feature.

## 23.2 THE DIMENSIONS OF REFLECTIVE METAPROGRAMMING

Previously, we described value metaprogramming based on constexpr evaluation and type metaprogramming based on recursive template instantiation. These two options, both available in modern C++, clearly involve different methods driving the computation. It turns out that value metaprogramming can also be driven in terms of recursive template instantiation, and prior to the introduction of constexpr functions in C++, that was the mechanism of choice. For example, the following code computes a square root of an integer using recursive instantiation:

[Click here to view code image](#)

```cpp
// primary template to compute sqrt(N)
template<int N, int Lo = 1, int Hi = N>
struct Sqrt {
  // compute the midpoint, rounded up
  static constexpr auto mid = (Lo + Hi + 1) / 2;

  // search a not too large value in a halved interval
  static constexpr auto value = (mid * mid > N)
      ? Sqrt<N, Lo, mid - 1>::value
      : Sqrt<N, mid, Hi>::value;
};

// partial specialization for the case when Lo equals Hi
template<int N, int M>
struct Sqrt<N, M, M> {
  static constexpr auto value = M;
};
```

This metaprogram uses much the same algorithm as our integer square root concept for function in Section 23.1 on page 253: successively halving an interval known to contain the square root. However, the input to the metaprogram is a compile-time argument instead of a function argument, and the “local variables” tracking the bounds to the interval are also now type template arguments. Clearly, this is a far less friendly approach than the constexpr function, but we will nevertheless analyze this idea later on to examine how it consumes compiler resources.

In any case, we can see that the computational engine of metaprogramming could potentially have many options. That is, however, not the only dimension in which such options may be considered. Instead, we like to think that a comprehensive metaprogramming solution for C++ must make choices along three dimensions:

- Computation
- Reflection
- Generation

*Reflection* is the ability to programmatically inspect features of the program. *Generation* refers to the ability to generate additional code for the program.

$\mathrm{Sqrt}<16,1,4>$ has a value of 4, as shown below:

```text
value = 4
```

$\mathrm{Sqrt}<16,1,4>$ value is decomposed as follows.

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_365_0.png)

```text
mid = (1 + 4 + 1) / 2
    = 3
value = $\mathrm{Sqrt}<16,3,4>$ value
      = $\mathrm{Sqrt}<16,4,4>$ value
```

Finally, $\mathrm{Sqrt}<16,3,4>$ value results in the following:

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_365_1.png)

```text
mid = (3 + 4 + 1) / 2
    = 4
value = $\mathrm{Sqrt}<16,4,4>$ value
```

and $\mathrm{Sqrt}<16,4,4>$ value ends the recursive process because it matches the explicit specialization that catches equal high and low bounds. The final result is therefore

```text
value = 4
```

### 23.3.1 Tracking All Instantiations

Our analysis above followed the significant instantiations that comprise the square root of 16. However, when a compiler evaluates the expression

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_365_2.png)

it instantiates not only the templates in the positive branch but also those in the negative branch ($\mathrm{Sqrt}<16,9,16>$). Furthermore, because the code attempts to access a member of the specialization using the `::` operator, all the members inside that class are also instantiated. This means that the full instantiation of $\mathrm{Sqrt}<16,9,16>$ results in the full instantiation of $\mathrm{Sqrt}<16,9,12>$. When the whole process is examined in detail, we find that dozens of instantiations end up being generated. The total number is almost twice the value of N.

Fortunately, there are techniques to reduce this explosion in the number of instantiations. To illustrate one such important technique, we rewrite our `Sqrt` metaprogram as follows:

![](img/58b3b6b55f5326ebb5db11acf6ac18cf_365_3.png)

```cpp
#include "ifthenelse.hpp"

// primary template for the recursive step
template<int N, int Low, int High>
struct Sqrt {
  // compute the midpoint, rounded up
  static constexpr auto mid = (Low + High + 1) / 2;

  // search a not too large value in a halved interval
  using Sub = typename ifThenElse<(mid * mid > N),
                                  Sqrt<N, Low, mid - 1>,
                                  Sqrt<N, mid, High>>::Type;
  static constexpr auto value = Sub::value;
};

// partial specialization for end of recursion criteria
template<int N, int Low>
struct Sqrt<N, Low, Low> {
  static constexpr auto value = Low;
};
```

The key change here is the use of the `ifThenElse` template, which was introduced in Section 9.1, on page 49. Remember, the `ifThenElse` template is a class that selects between two types based on a given Boolean constant. If the constant is true, the first type is instantiated; otherwise, the second type is instantiated.

An instance does not cause a C++ compiler to instantiate the body of that instance. Therefore, when we write

```cpp
using S = ...;
S<T1, T2, ...>;
S<T2, T1, ...>;
```

neither `S<T1, T2, ...>` nor `S<T2, T1, ...>` is fully instantiated. Whichever of these two types ends up being an argument for `ifThenElse` is fully instantiated when looking up `Sub` in the context of `Sqrt`'s body. An important point: this strategy leads to a number of instantiations that is proportional to log(n), a very significant reduction in the cost of metaprogramming when compared to recursive instantiation.

## 23.4 COMPUTATIONAL COMPLETENESS

Our GCD example demonstrates that a template metaprogram can contain:

- State variables: The template parameters
- Loop constructs: Through recursion
- Execution path selection: By using conditional expressions or specializations
- Integer arithmetic

If there are no limits to the amount of recursive instantiations and the number of state variables that are allowed, it can be shown that this is sufficient to compute anything that is computable. However, it may not be convenient to do so using templates. Furthermore, because template instantiation requires substantial compiler resources, extensive recursive instantiation quickly slows down a compiler or even exhausts the resources available. The C++ standard recommends but does not mandate that a minimum of 1024 levels of recursive instantiations be allowed, which is sufficient for most (but certainly not all) template metaprogramming tasks.

Hence, in practice, template metaprograms should be used sparingly. There are a few situations, however, when they are increasingly used to implement convenient templates. In particular, they can sometimes be hidden in the innards of more conventional templates to secure more performance out of critical algorithms.

## 23.5 RECURSIVE INSTANTIATION VERSUS RECURSIVE TEMPLATE ARGUMENTS

Consider the following recursive template:

[Click here to view code image](#)

```cpp
template<typename T, typename U>
struct Doubly {
};

template<int N>
struct Trouble {
    using LongType = Doubly<Trouble<N-1>, Trouble<N-1>>;
};

template<>
struct Trouble<0> {
    using LongType = double;
};
```

The use of `Trouble<3>::LongType` not only triggers the recursive instantiation of `Trouble<3>`, `Trouble<2>`, ..., `Trouble<0>`, but it also instantiates `Doubly` if every increasingly complex type. Table 23.1 illustrates how quickly it grows.

| Type Alias | Underlying Type |
|---|---|
| `Trouble<0>::LongType` | `double` |
| `Trouble<1>::LongType` | `Doubly<double, double>` |
| `Trouble<2>::LongType` | `Doubly<Doubly<double, double>, Doubly<double, double>>` |
| `Trouble<3>::LongType` | `Doubly<Doubly<Doubly<double, double>, Doubly<double, double>>, Doubly<Doubly<double, double>, Doubly<double, double>>>` |

Table 23.1: Growth of `Trouble<N>::LongType`

As can be seen from Table 23.1, the complexity of the type description of the expression `Trouble<N>::LongType` grows exponentially with N. In general, such a situation occurs in C++ compilers even more than do recursive instantiations that do not involve recursive arguments. One of the problems here is that a compiler keeps a representation of the
