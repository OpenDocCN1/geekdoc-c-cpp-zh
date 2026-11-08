
called the **point of instantiation (POI)**, dependent qualified names are looked up (with the template parameters replaced with the template arguments for that specific instantiation), and an additional ADL is performed for the unqualified dependent names that were looked up using ordinary lookup.

For qualified dependent names, the initial ordinary lookup—while not complete—is used to decide whether the name is a template. Consider the following example.

```cpp
template<typename T>
void g() {
  typename T::X x;
}

template<typename T>
void f() {
  g<int>();
}

int main() {
  f<int>(); // calls template f with T = int
}
```

In line 7, when seeing the name `T` followed by a `<`, the compiler has to decide whether that `<` is an angle bracket or a less-than sign. That decision depends on whether `T` is known to be the name of a template or not; in this case, ordinary lookup finds the declaration of `T`, which is a struct with a type, and so parsing succeeds with angle brackets.

Line 9, however, produces an error because no template is found using ordinary lookup: the `<` is thus treated as a less-than sign, which is a syntax error in this example. If we could get past this issue, we'd eventually find the template using ADL, when instantiating `f<int>`.

### 14.3.2 Points of instantiation

We have already illustrated that there are points in the source of template clients where a C++ compiler must have access to the declaration or the definition of a template entity. A point of instantiation (POI) is created when a code construct refers to a template specialization in such a way that the definition of the corresponding template needs to be instantiated to create that specialization. The POI is a point in the source where the substituted template could be inserted. For example:

```cpp
class MyInt {
public:
  MyInt(int i);
};

MyInt operator - (MyInt const&);

bool operator > (MyInt const&, MyInt const&);

using Int = MyInt;

template<typename T>
void f(T t)
{
  if (t > 0)
    g(-1);
}

// #1
void g(int);

// #2
f<Int>(42);  // point of call

// #3
// #4
```

At the point at which `f<Int>(42)` is instantiated, it knows that the template `f` will need to be instantiated for `T` substituted with `Int`. A POI is created. POI #2 is the very same point as the point of call, but they cannot be the same point because C++ does not allow to insert the definition of `f` at the point of call.

The template definition is instantiated at the point where the template is needed. The compiler must therefore find the declaration of `g` through the appropriate lookup rules. The call `g(-1)` is dependent and is looked up both at the template definition and at the point of instantiation.

If we now wonder why this example involved the type `MyInt` rather than simple `Int`, the answer lies in the fact that the second lookup performed at the POI is only an ADL. Because `Int` is not an associated namespace, the compiler would therefore not be able to find the plain `g` and would not find the function `g`. Hence, if we were to replace the type alias declaration for `Int` with

`using Int = int;`

the previous example would no longer compile. The following example suffers from a similar problem:

```cpp
g1(x);  // #1

void g1(int)
{
}

int main()
{
    f1();  // ERROR: g1 not found!
}  // #2
```

The call of f1() creates a POI for f1<int> just outside of main() at point #3. In this instantiation, the key issue is the lookup of function g1. When the definition of the template f1 is first encountered, it is noted that the unqualified name g1 is dependent because it is the name of a function in a function call with dependent arguments (the type of the argument depends on the template parameter). Therefore, g1 is looked up at point #4 using ordinary lookup now; however, no g1 is visible at this point. At point #2, the function is looked up again via associated classes and namespaces, but the only argument type is int, and it has no associated namespaces and classes. Therefore, g1 is never found even though ordinary lookup at the POI would have found g1.

The point of instantiation for variable templates is handled similarly to that of function templates. For class template specialization, the situation is different, as the following example illustrates:

```cpp
template<typename T>
class C {
  public:
    T m;
};

// #1
unsigned long f()
{
    // #2
    return sizeof(C<int>);
} // #3
```

Again, the function scope points #2 and #3 cannot be POIs because a definition of a namespace-scope class C<int> cannot appear there (and templates can generally not appear in function scope). If we were to follow the rule for function template instantiations, the POI would be at point #4, but then the expression sizeof(C<int>) is invalid because the size of C<int> cannot be determined until point #4 is reached. Therefore, the POI for a reference to a generated class instance is defined to be the point immediately before a point that is defined to be the point of instantiation of the definition that contains the reference to that instance. In our example, this is point #4.

When a template is actually instantiated, the need for additional instantiations may appear. Consider a short example:

```cpp
template<typename T>
class S {
  public:
    using A = int;
};

// #1
template<typename T>
void f(T val = 41);
template<typename T>
void f(T val = 42);

int main()
{
    f<double>();
} // #2
```

Our preceding discussion already established that the POI for f<double> is at point #2. In function f(), the function template f is also instantiated at point #3. It references the class specialization S<double>, which is therefore at point #3. If references to the class specialization S<double> are needed before the point of instantiation, the class must be instantiated earlier.

A translation unit often contains multiple POIs for the same instance. For example, the following example contains multiple POIs for the same instantiation. In such a case, the instantiation occurs at a point determined by the rules for POIs. For instances of function and variable templates, all POIs are merged. In either case, the ODR requires that the instantiation occurs only at one of the merged POIs. The compiler chooses the POI according to a variety of rules, defined by the standard. This allows a compiler to pick just one nonclass POI to perform the actual instantiation without worrying that another POI might result in a different instantiation.

templates to the end of the translation unit. Some instantiations cannot be delayed, including cases where instantiation is needed to determine a deduced return type (see Section 15.10.1 on page 296 and Section 15.10.4 on page 303) and cases where the function is constexpr and must be evaluated to produce a constant result. Some compilers instantiate inline functions when they’re first used to potentially inline the call right away.

This effectively moves the POIs of the corresponding template specializations to the end of the translation unit, which is permitted by the C++ standard as an alternative POI.

### 14.3.3 The Inclusion Model

Whenever a POI is encountered, the definition of the corresponding template must somehow be accessible. For class specialization this means that the class template definition must have been seen earlier in the translation unit. For the POIs of function and variable templates (and member functions and static data members of class templates) this is also needed, and typically template definitions are simply added to header files that are included in the translation unit, even when they’re not the only template definitions in that file. This source model for template definitions is called the inclusion model, and it is the only automatic source model for templates supported by the current C++ standard.

Although the inclusion model encourages programmers to place all their template definitions in header files so that they are available to satisfy any POIs that may arise, it is also possible to explicitly manage instantiations using explicit instantiation declarations and explicit instantiation definitions (see Section 14.5.0 on page 260). Doing so is logically out of the question and most of the time programmers will prefer to rely on the automatic instantiation mechanism instead. One challenge for an implementation with the automatic scheme is to deal with the possibility of having POIs for the same specialization at different points (or the same member function or static data member of a class template instance) across different translation units. We discuss approaches to this problem next.

## 14.4 IMPLEMENTATION SCHEMES

In this section we review some ways in which C++ implementations support the inclusion model. All these implementations rely on two classic components: a compiler and a linker. The compiler translates source code to object files, which contain machine code with symbolic annotations (cross-referencing other object files and libraries). The linker creates executable programs or libraries by combining the object files and resolving the symbolic cross-references they contain. In what follows, we assume such a model even though it is entirely possible (but not popular) to implement C++ in other ways. For example, one might imagine a C++ interpreter.

When a class template specialization is used in multiple translation units, a compiler will repeat the instantiation process in every translation unit. This poses very few problems because definitions do not directly create object-level code. They are used only internally by a C++ implementation to verify and interpret various other expressions and declarations. In this regard, the multiple instantiations of a class definition are not materially different from the multiple inclusions of a class definition—typically through header file inclusion—in various translation units.

However, if we instantiate a non-inline function template, the situation may be different. If you were to provide multiple definitions of an ordinary, non-inline function, you would violate the ODR. Assume, for example, that you compile and link a program consisting of the following two files:

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

C++ compilers will compile each module separately without any problems because indeed they are valid C++ translation units. However, your linker will most likely reject if you try to link the two together. Duplicate definitions are not allowed.

In contrast, consider the template case:

```cpp
// ------ a.hpp:
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
