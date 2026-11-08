templates to the end of the translation unit. Some instantiations cannot be delayed, including cases where instantiation is needed to determine a deduced return type (see Section 15.10.1 on page 296 and Section 15.10.4 on page 303) and cases where the function is constexpr and must be evaluated to produce a constant result. Some compiler instantiations inline functions when they’re first used to potentially inline the call right away.

This effectively moves the POIs of the corresponding template specializations to the end of the translation unit, which is permitted by the C++ standard as an alternative POI.

# ### 14.3.3 The Inclusion Model

Whenever a POI is encountered, the definition of the corresponding template must somehow be accessible. For class specialization this means that the class template definition must have been seen earlier in the translation unit. For the POIs of function and variable templates (and member functions and static data members of class templates) this is also needed, and typically template definitions are simply added to header files that are included in the translation unit, even when they’re not the only template definitions in that file. This source model for template definitions is called the inclusion model, and it is the only automatic source model for templates supported by the current C++ standard.

Although the inclusion model encourages programmers to place all their template definitions in header files so that they are available to satisfy any POIs that may arise, it is also possible to explicitly manage instantiations using explicit instantiation declarations and explicit instantiation definitions (see Section 14.5.0 on page 260). Doing so is logically out of mind and most of the time programmers will prefer to rely on the automatic instantiation mechanism instead. One challenge for an implementation with the automatic scheme is to deal with the possibility of having POIs for the same specialization at different template (or the same member function or static data member of a class template instance) across different translation units. We discuss approaches to this problem next.

# ## 14.4 IMPLEMENTATION SCHEMES

In this section we review some ways in which C++ implementations support the inclusion model. All these implementations rely on two classic components: a compiler and a linker. The compiler translates source code to object files, which contain machine code with symbolic annotations (cross-referencing other object files and libraries). The linker creates executable programs or libraries by combining the object files and resolving the symbolic cross-references they contain. In what follows, we assume such a model even though it is entirely possible (but not popular) to implement C++ in other ways. For example, one might imagine a C++ interpreter.

When a class template specialization is used in multiple translation units, a compiler will repeat the instantiation process in every translation unit. This poses very few problems because definitions do not directly create at-level code. They are used only internally by a C++ implementation to verify and interpret various other expressions and declarations. In this regard, the multiple instantiations of a class definition are not materially different from the multiple inclusions of a class definition—typically through header file inclusion—in various translation units.

However, if we instantiate a non-inline function template, the situation may be different. If you were to provide multiple definitions of an ordinary, non-inline function, you would violate the ODR. Assume, for example, that you compile and link a program consisting of the following two files:

```
```cpp
// ------ a.cpp:
int main()
{
  f();
}

// ------ b.cpp:
int main()
{
  f();
}
```
```

C++ compilers will compile each module separately without any problems because indeed they are valid C++ translation units. However, your linker will most likely reject if you try to link the two together. Duplicate definitions are not allowed.

In contrast, consider the template case:

Click here to view code image

```
```cpp
// ------ a.cpp:
// common header (inclusion model?)
#include <a.hpp>
class S {
public:
  void f();
};

template<typename T>
void S<T>::f()    // member definition
{
}

void helper(S<int>*);
// ------ a.cpp:
#include "a.hpp"
void helper(S<int>* a)
{
  a->f();    // #1 first point of instantiation of S::f
}

// ------ b.cpp:
#include "b.hpp"
int main()
```
```