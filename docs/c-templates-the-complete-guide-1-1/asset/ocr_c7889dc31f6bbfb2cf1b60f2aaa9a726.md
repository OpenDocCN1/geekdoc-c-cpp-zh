```
```cpp
void f() {
    D<int> d = 0;
};

#ifndef LAST
#define LAST 10
#endif

int main()
{
    Print_pointer<D> a;
    a.f();
}
```
```

If you compile this program, the compiler will print error messages when, in `pointer<int>()`, the initialization of `d` fails. This happens when the initial value is `1` because there is only a constructor for `void*`, and only one has a valid conversion to `void*`. For example, on one compiler, we get (among several other messages) the following errors:

[Click here to view code image](#)

```
```text
ut.cpp:35:14: error: no viable conversion from 'const
int*' to 'D<int>'
ut.cpp:39:14: error: no viable conversion from 'const
int*' to 'D<int>'
ut.cpp:39:14: error: no viable conversion from 'const
int*' to 'D<int>'
ut.cpp:39:14: error: no viable conversion from 'const
int*' to 'D<int>'
ut.cpp:39:14: error: no viable conversion from 'const
int*' to 'D<int>'
```
```

The concept of C++ template metaprogramming as a serious programming tool was first made popular (and somewhat formalized) by Todd Veldhuizen in his paper *Using C++ Template Metaprograms* [Todd's work on Blitz++ (a numeric array library for C++, see [Blitz++](#)) also introduced many refinements and extensions to metaprogramming (and to expression template techniques, introduced in Chapter 27).]

Both the first edition of this book and Andrei Alexandrescu's *Modern C++ Design* (see [AlexandrescuDesign](#)) contributed to an explosion of C++ libraries exploiting template-based metaprogramming by exploiting some of the basic techniques that are still in use today. The Boost project (see [Boost](#)) was instrumental in bringing order to this explosion. Early on, it introduced the MPL (meta-programming library), which defined a consistent framework for meta-metaprogramming made popular through Alexandrescu and Gurtovoy's book *C++ Template Metaprogramming* (see [Boost.MPL](#)).

Additional important advances have been made by Louis Dionne in making metaprogramming syntactically more accessible, particularly through his Boost.Hana library (see [Boost.Hana](#)). Louis, along with Andrew Sutton, Herb Sutter, David Vandevoorde, and others are now spearheading efforts in the standardization committee to give metaprogramming first-class support in the language. An important basis for that work is the exploration of what programming idioms can be enabled through reflection; Matúš Chochlík, Axel Naumann, and David Sankel are principal contributors in that area.

In *[Itertools](#)* John R. Burton and Lee R. Nackman illustrated how to keep track of dimensional units when performing computations. The *Stanford Library* was a more comprehensive library for dealing with physical units developed by Walter Brown ([Boost.Units](#)). The `std::chrono` component in the standard library, which we used as an illustration for Section 3.1.1 on page 534, is only the most convenient and less quantitated by Howard Hinnant.

+   1. The C++11 `constexpr` capabilities were sufficient to solve many concerns (e.g., no loop statements were available, making it very hard to explain recursive function calls; see Section 2.3 on page 59). C++14 enabled loop statements and various other constructs.
+   
+   2. The C++ standard library provides a corresponding type trait `std::remove_all_extents`. See Section 4.4 on page 70 for details.
+   
+   3. This is known as *loop unrolling*. We generally recommend against explicitly unrolling loops in portable code since the details that determine the best unrolling strategy depend highly on the target platform and the loop body; the compiler usually does a much better job of taking those