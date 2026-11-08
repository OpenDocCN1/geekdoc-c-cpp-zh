matically inspect features of the program (e.g., answering questions such as Is type an integer? or What monotonic data members does a class type contain?). Metaprogramming is the craft of “programming the program,” which usually amounts to programmatically generating new code. Reflective metaprogramming, then, is the craft of automatically analyzing code that adapts itself to existing properties (often, type(s) of a program).

In Part II of this book, we will explore how boundary conditions can serve some simple forms of reflection and metaprogramming (in some sense, template instantiation is a form of metaprogramming, because it creates the synthesis of two or more types from a form of template).

According to the potential of such facilities in this area, the C++ standardization committee created a study group (SG7) to explore options for more powerful reflection. That group’s charter was later extended to cover metaprogramming too. Here is an example of the aspects being considered:

Click here to view code image

```
```cpp
template<typename T> void report(T p) {
  constexpr
    // reflection and metaprogramming facilities
    // ...

  // code will be injected here
}
```
```

Quite a few new things are present in this code. First, the constexpr(...) construct forces the statements in it to be evaluated at compile time, but if it appears in a template, this evaluation is only done when the template is instantiated. Second, the decltype operator produces an expression of opaque type. Once the details of reflection are available in the reflection library, this can be used to obtain information about the type’s data members and member functions. This metaprogram produces a sequence of objects describing the direct nonstatic data members of the type or class. So far the loop above is really a loop over the nonstatic data members of the type. The compiler can then use this information to produce a sequence of data members.

Click here to view code image

```
```cpp
struct X {
  int x;
  std::string s;
};
```
```

would produce an instantiation similar to

Click here to view code image

```
```cpp
template<typename T> ...
{
  std::cout << "x" << ...;
  std::cout << "s" << ...;
}
```
```

That is, this function automatically generates a function to output the nonstatic data member values of a class type.

There are many possibilities for these types of capabilities. While it is likely that something like this will eventually be adopted into the language, it is unclear in what time frame it can be expected. That said, a few experimental implementations of such systems have been demonstrated at the time of this writing, but before going to press with this book, SG7 agreed on the general direction of using constexpr evaluation and a value metaobject table instead of a kind of fixed reflection metaprogramming. The injection mechanism presented here, however, was not agreed on, and most likely a different system will be pursued.

# 17.10 PACK FACILITIES

Parameter packs were introduced in C++11, but dealing with them often requires recursive template instantiation techniques. Recall this routine of code discussed in Section 14.6 on page 926:

Click here to view code image

```
```cpp
// code continues below the visible area
```
```