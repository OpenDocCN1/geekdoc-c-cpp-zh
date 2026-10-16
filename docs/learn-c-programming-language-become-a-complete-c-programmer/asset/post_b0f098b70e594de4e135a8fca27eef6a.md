
### 26.2.2 Manual Control of Instantiation

```cpp
template int convert<int,double>; // syntax error
```

As in template function calls, the template arguments that can be deduced from the function arguments can be omitted (§23.5.1). For example:

```cpp
template int convert<int,double>(double); // OK (redundant)
template int convert<int>(double); // OK
```

When a class template is explicitly instantiated, every member function is also instantiated. The link-time and recompilation efficiency impact of instantiation requests can be significant. I have seen examples in which bundling most template instantiations into a single compilation unit cut the compile time from a number of hours to the equivalent number of minutes. It is an error to have two definitions for the same specialization. It does not matter if such multiple specializations are user-defined (§25.3), implicitly generated (§23.2.2), or explicitly requested.

However, a compiler is not required to diagnose multiple instantiations in separate compilation units. This allows a smart implementation to ignore redundant instantiations and thereby avoid problems related to composition of programs from libraries using explicit instantiation. However, implementations are not required to be smart. Users of “less smart” implementations must avoid multiple instantiations. The worst that will happen if they don’t is that their program won’t link; there will be no silent changes of meaning.

To complement explicit instantiation requests, the language provides explicit requests not to instantiate (usually called extern templates). The obvious use is to have one explicit instantiation for a specialization and use extern templates for its use in other translation units. This mirrors the classical use of one definition and many declarations (§15.2.3). For example:

```cpp
#include "MyVector.h"

extern template class MyVector<int>; // suppresses implicit instantiation
// explicitly instantiate elsewhere

void foo(MyVector<int>& v) {
    // ... use the vector in here ...
}
```

The “elsewhere” might look something like this:

```cpp
#include "MyVector.h"

template class MyVector<int>; // instantiate in this translation unit; use this point of instantiation
```

In addition to generating specializations for all members of a class, the explicit instantiation also determines a single point of instantiation so that other points of instantiation (§26.3.3) can be ignored. One use of this is to place the explicit instantiation in a shared library.

## 26.3 Name Binding

Define template functions to minimize dependencies on nonlocal information. The reason is that a template will be used to generate functions and classes based on unknown types and in unknown contexts. Every subtle context dependency is likely to surface as a problem for somebody – and that somebody is unlikely to want to know the implementation details of the template. The general rule of avoiding global names as much as possible should be taken especially seriously in template code. Thus, we try to make template definitions as self-contained as possible and to supply much of what would otherwise have been global context in the form of template arguments (e.g., traits; §28.2.4, §33.1.3). Use concepts to document dependencies on template arguments (§24.3).

However, it is not unusual that some nonlocal names must be used to achieve the most elegant formulation of a template. In particular, it is more common to write a set of cooperating template functions than to write just one self-contained function. Sometimes, such functions can be class members, but not always. Sometimes, nonlocal functions are the best choice. Typical examples of that are sort()’s calls to swap() and less() (§25.3.4). The standard-library algorithms are a large-scale example (Chapter 32). When something needs to be nonlocal, prefer a named namespace to the global scope. Doing so preserves some locality.

Operations with conventional names and semantics, such as +, *, [], and sort(), are another source of nonlocal name use in a template definition. Consider:

```cpp
bool tracing;
template<typename T> T sum(std::vector<T>& v) {
    T t {};
    if (tracing)
        cerr << "sum(" << &v << ")\n";
    for (int i = 0; i != v.size(); i++)
        t = t + v[i];
    return t;
}
// ...
#include <quad.h>
void f(std::vector<Quad>& v) {
    Quad c = sum(v);
}
```

The innocent-looking template function sum() depends on several names that are not explicitly specified in its definition, such as tracing, cerr, and the + operator. In this example, + is defined in <quad.h>:

```cpp
Quad operator+(Quad,Quad);
```

Importantly, nothing related to Quad is in scope when sum() is defined, and the writer of sum() cannot be assumed to know about class Quad. In particular, the + may be defined later than sum() in the program text, and even later in time.

The process of finding the declaration for each name explicitly or implicitly used in a template is called *name binding*. The general problem with template name binding is that three contexts are involved in a template instantiation and they cannot be cleanly separated:

- [1] The context of the template definition
- [2] The context of the argument type declaration
- [3] The context of the use of the template

When defining a function template, we want to assure that enough context is available for the template definition to make sense in terms of its actual arguments without picking up “accidental stuff” from the environment of a point of use. To help with this, the language separates names used in a template definition into two categories:

- [1] *Dependent names*: names that depend on a template parameter. Such names are bound at a point of instantiation (§26.3.3). In the **sum()** example, the definition of + can be found in the instantiation context because it takes operands of the template argument type.

- [2] *Nondependent names*: names that don’t depend on a template parameter. Such names are bound at the point of definition of the template (§26.3.2). In the **sum()** example, the template **vector** is defined in the standard header `<vector>`, and the Boolean **tracing** is in scope when the definition of **sum()** is encountered by the compiler.

To be considered, both dependent and independent names must either be in scope at their point of use or be found by argument-dependent lookup (ADL; §14.2.4).

The following subsections go into considerable technical detail about how dependent and nondependent names in a template definition are bound for a specialization. For complete details, see §iso.14.6.

### 26.3.1 Dependent Names

The simplest definition of “**N** depends on a template parameter **T**” would be “**N** is a member of **T**.” Unfortunately, this doesn’t quite suffice; addition of `Quad`s (§26.3) is a counter-example.

Consequently, a function call is said to *depend on* a template argument if and only if one of these conditions holds:

- [1] The type of the actual argument depends on a template parameter **T** according to the type deduction rules (§23.5.2), for example, **f(T(1))**, **f(t)**, **f(g(t))**, and **f(&t)**, assuming that **t** is a **T**.

- [2] The function called has a parameter that depends on **T** according to the type deduction rules (§23.5.2), for example, **f(T)**, **f(list<T>&)**, and **f(const T\*)**.

Basically, the name of a called function is dependent if it is obviously dependent by looking at its arguments or at its formal parameters. For example:

```cpp
template<typename T>
T f(T a)
{
    return g(a); // OK: a is a dependent name and therefore so is g
}
class Quad { /*...*/ };
void g(Quad);
int z = f(Quad{2}); // f’s g is bound to g(Quad)
```

A call that by coincidence has an argument that matches an actual template parameter type is not dependent. For example:

```cpp
class Quad { /*...*/ };

template<typename T> T ff(T a)
{
    return gg(Quad{1}); // error: no gg() in scope and gg(Quad{1}) doesn’t depend on T
}
int gg(Quad);

int zz = ff(Quad{2});
```

Had gg(Quad{1}) been considered dependent, its meaning would have been most mysterious to a reader of the template definition. If a programmer wants gg(Quad) to be called, gg(Quad)’s declaration should be placed before the definition of ff() so that gg(Quad) is in scope when ff() is analyzed. This is exactly the same rule as for non-template function definitions (§26.3.2).

By default, a dependent name is assumed to name something that is not a type. So, to use a dependent name as a type, you have to say so, using the keyword typename. For example:

```cpp
template<typename Container>
void fct(Container& c)
{
    Container::value_type v1 = c[7]; // syntax error: value_type is assumed to be a non-type name
    typename Container::value_type v2 = c[9]; // OK: value_type assumed to name a type
    auto v3 = c[11]; // OK: let the compiler figure it out
    // ...
}
```

We can avoid such awkward use of typename by introducing a type alias (§23.6). For example:

```cpp
template<typename T>
using Value_type = typename T::value_type;

template<typename Container>
void fct2(Container& c)
{
    Value_type<Container> v1 = c[7]; // OK
    // ...
}
```

Naming a member template after a . (dot), ->, or :: requires similar use of the keyword template. For example:

```cpp
class Pool { // some allocator
public:
    template<typename T> T* get();
    template<typename T> void release(T*);
    // ...
};
```
