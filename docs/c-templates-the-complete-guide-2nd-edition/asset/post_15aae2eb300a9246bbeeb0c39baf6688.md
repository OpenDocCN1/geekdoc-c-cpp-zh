
Over 10,000 characters for `Trouble<10>::LongType`. Newer C++ implementations take into account the fact that nested template-ids are fairly common in modern C++ programs and use clever compression techniques to reduce considerably the growth in name encoding (e.g., a few hundred characters for `Trouble<10>::LongType`). These newer compilers also avoid generating a mangled name if none is actually needed because no low-level code is actually generated for the template instance. Still, all other things being equal, it is probably preferable to organize recursive instantiation in such a way that template arguments need not also be nested recursively.

## 23.6 Enumeration Values versus Static Constants

In the early days of C++, enumeration values were the only mechanism to create “true constants” (called *constant-expressions*) as named members in class declarations. With them, we could, for example, define a Pow3 metaprogram to compute powers of 3 as follows: [Click here to view code image](#)

```
meta/pow3enum.hpp

// primary template to compute 3 to the Nth
template<int N>
struct Pow3 {
enum { value = 3 * Pow3<N-1>::value };
};
// full specialization to end the recursion
template<>
struct Pow3<0> {
enum { value = 1 };
};
```

The standardization of C++98 introduced the concept of in-class static constant initializers, so that our Pow3 metaprogram could look as follows: [Click here to view code image](#)

```
meta/pow3const.hpp

// primary template to compute 3 to the Nth
template<int N>
struct Pow3 {
static int const value = 3 * Pow3<N-1>::value;
};

// full specialization to end the recursion
template<>
struct Pow3<0> {
static int const value = 1;
};
```

However, there is a drawback with this version: Static constant members are lvalues (see Appendix B). So, if we have a declaration such as void foo(int const&); and we pass it the result of a metaprogram: foo(Pow3<7>::value); a compiler must pass the address of Pow3<7>::value, and that forces the compiler to instantiate and allocate the definition for the static member. As a result, the computation is no longer limited to a pure “compile-time” effect.

Enumeration values aren’t lvalues (i.e., they don’t have an address). So, when we pass them by reference, no static memory is used. It’s almost exactly as if you passed the computed value as a literal. The first edition of this book therefore preferred the use of enumerator constants for this kind of applications.

C++11, however, introduced constexpr static data members, and those are not limited to integral types. They do not solve the address issue raised above, but in spite of that shortcoming they are now a common way to produce results of metaprograms. They have the advantage of having a correct type (as opposed to an artificial enum type), and that type can be deduced when the static member is declared with the auto type specifier. C++17 added inline static data members, which do solve the address issue raised above, and can be used in conjunction with constexpr.

## 23.7 Afternotes

The earliest documented example of a metaprogram was by Erwin Unruh, then representing Siemens on the C++ standardization committee. He noted the computational completeness of the template instantiation process and demonstrated his point by developing the first metaprogram. He used the Metaware compiler and coaxed it into issuing error messages that would contain successive prime numbers. Here is the code that was circulated at a C++ committee meeting in 1994 (modified so that it now compiles on standard conforming compilers):⁶

[Click here to view code image](#)

```
meta/unruh.cpp

// prime number computation
// (modified from original from 1994 by Erwin Unruh)

template<int p, int i>
struct is_prime {
enum { pri = (p==2) || ((p%i) && is_prime<(i>2?p:0),i-1>::pri) };
};

template<>
struct is_prime<0,0> {
enum {pri=1};
};

template<>
struct is_prime<0,1> {
enum {pri=1};
};

template<int i>
struct D {
D(void*);
};

template<int i>
struct CondNull {
static int const value = i;
};
template<>
struct CondNull<0> {
static void* value;
};
void* CondNull<0>::value = 0;

template<int i>
struct Prime_print { // primary template for loop to print prime numbers
Prime_print<i-1> a;
enum { pri = is_prime<i,i-1>::pri };
void f() {
D<i> d = CondNull<pri ? 1 : 0>::value; // 1 is an error, 0 is fine
a.f();
}
};

template<>
struct Prime_print<1> { // full specialization to end the loop
enum {pri=0};
void f() {
D<1> d = 0;
};
};

#ifndef LAST
#define LAST 18
#endif

int main()
{
Prime_print<LAST> a;
a.f();
}
```

If you compile this program, the compiler will print error messages when, in Prime_print::f(), the initialization of d fails. This happens when the initial value is 1 because there is only a constructor for void*, and only 0 has a valid conversion to void*. For example, on one compiler, we get (among several other messages) the following errors:⁷

[Click here to view code image](#)

```
unruh.cpp:39:14: error: no viable conversion from 'const int' to 'D<17>'
unruh.cpp:39:14: error: no viable conversion from 'const int' to 'D<13>'
unruh.cpp:39:14: error: no viable conversion from 'const int' to 'D<11>'
unruh.cpp:39:14: error: no viable conversion from 'const int' to 'D<7>'
unruh.cpp:39:14: error: no viable conversion from 'const int' to 'D<5>'
unruh.cpp:39:14: error: no viable conversion from 'const int' to 'D<3>'
unruh.cpp:39:14: error: no viable conversion from 'const int' to 'D<2>'
```

The concept of C++ template metaprogramming as a serious programming tool was first made popular (and somewhat formalized) by Todd Veldhuizen in his paper Using C++ Template Metaprograms (see [VeldhuizenMeta95]). Todd’s work on Blitz++ (a numeric array library for C++, see [Blitz++]) also introduced many refinements and extensions to metaprogramming (and to expression template techniques, introduced in Chapter 27).

Both the first edition of this book and Andrei Alexandrescu’s “Modern C++ Design” (see [AlexandrescuDesign]) contributed to an explosion of C++ libraries exploiting template-based metaprogramming by cataloging some of the basic techniques that are still in use today. The Boost project (see [Boost]) was instrumental in bringing order to this explosion. Early on, it introduced the MPL (meta-programming library), which defined a consistent framework for type *metaprogramming* made popular also through Abrahams and Gurtovoy’s book “C++ Template Metaprogramming” (see [*Boost-MPL*]).

Additional important advances have been made by Louis Dionne in making metaprogramming syntactically more accessible, particularly through his Boost.Hana library (see [*BoostHana*]). Louis, along with Andrew Sutton, Herb Sutter, David Vandevoorde, and others are now spearheading efforts in the standardization committee to give metaprogramming first-class support in the language. An important basis for that work is the exploration of what program properties should be available through reflection; Matúš Chochlík, Axel Naumann, and David Sankel are principal contributors in that area.

In [*BartonNackman*] John J. Barton and Lee R. Nackman illustrated how to keep track of dimensional units when performing computations. The *SIunits* library was a more comprehensive library for dealing with physical units developed by Walter Brown ([*BrownSIunits*]). The `std::chrono` component in the standard library, which we used as an inspiration for Section 23.1.4 on page 534, only deals with time and dates, and was contributed by Howard Hinnant.

¹ The C++11 constexpr capabilities were sufficient to solve many common challenges, but the programming model was not always pleasant (e.g., no loop statements were available, so iterative computation had to exploit recursive function calls; see Section 23.2 on page 537). C++14 enabled loop statements and various other constructs.

² The C++ standard library provides a corresponding type trait `std::remove_all_extents`. See Section D.4 on page 730 for details.

³ This is known as *loop unrolling*. We generally recommend against explicitly unrolling loops in portable code since the details that determine the best unrolling strategy depend highly on the target platform and the loop body; the compiler usually does a much better job of taking those considerations into account.

⁴ We specify the `inline` keyword explicitly here because some compilers (notably Clang) take this as hint to try a little harder to inline calls. From a language point of view, these functions are implicitly `inline` because they are defined in the body of their enclosing class.

⁵ Some of the traits provided in the C++ standard library already rely on some cooperation from the compiler (via nonstandard “intrinsic” operators). See Section 19.10 on page 461.

⁶ Thanks to Erwin Unruh for providing the code for this book. You can find the
