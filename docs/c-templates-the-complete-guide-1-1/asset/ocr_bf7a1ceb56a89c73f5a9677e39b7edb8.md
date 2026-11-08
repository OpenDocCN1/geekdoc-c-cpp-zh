```
```cpp
class Vector {
public:
    ...
    void pod() {}
    T* xp; // declaration of multiplication?
    ...
};

template<>
class Trapezoid : public Vector {
public:
    void f(int) {}
    // Error: no type here
};

void f(Vector& v, bool b)
{
    v.pod(); // OK
}
```
```

At the compiler is parsing line 42, it must decide whether it is declaring a declaration or a multiplication. This decision in turn depends on whether the dependent qualified name Trapezoid<T>::x is a type name. It may be tempting to look in the template at the point at and first, and assuming line 41, T* x is a type and x is what would be chosen if there were no specialization. However, a rule to this effect would make the following code invalid (we show this in this case where v is valid). In this case, T is a template. In this case, T::x is a dependent type because the type depends on the template parameter. Moreover, T::x refers to an unknown specialization described in Section 13.2.4 on page 220, which means that the compiler cannot safely look inside the template to determine whether the name Trapezoid<T>::x is a type or not. Had the code specified at line 42, T::x is a type. If the second x is valid? See, but the compiler could have looked up the template definition before it examines in another or that specialization could intervene. Also, when the parsing code is entered, the entire translation unit is available in memory. Also, when the parsing code is entered, the entire translation unit is available in memory. However, the compiler has to parse the entire translation unit in order to understand the meaning. This task would be enormous if it required the compiler to parse all the template definitions each time it encountered a template-id. Therefore, the compiler parses a template-id is equivalent to a qualified name lookup for nondependent types.

However, as illustrated by the example, name lookup into an unknown specialization is still a problem. The language definition addresses this issue by stating that names in a template definition are assumed not to name types unless a type name is defined with the keyword typename. If, thus fails, or without rebinding template arguments, the name is not the name of a type, the program is ill-formed and your C++ compiler should complain at instantiation time. Note that this rule does not provide any help; it just gives an indication as to whether a type is involved. The typename prefix to a name is required when the name satisfies all of the following conditions:

+   1. It is qualified and not itself followed by :: to form a more-qualified name.
+   2. It is not part of an elaborated-type-specifier (i.e., a type name that starts with one of the keywords class, struct, union, or enum).
+   3. It is not used in a base class specification or in a list of member initializers (including a mem-initializer).
+   4. It is dependent on a template parameter.
+   5. It is a member of an unknown specialization, meaning that the type named by the qualified name refers to an unknown specialization.

Performance: the typename prefix is not allowed unless at least the first two previous conditions hold. To illustrate this, consider the following erroneous example:

Click here to view code image

```
```cpp
template<typename T>
struct S {
    typedef int X;
};
template<typename T>
class C {
    typename T::X x1; // declaration of pointer
    typename T::X x2; // multiplication?
    S<int>::X x3;
    typename S<int>::X x4;
};
typedef int Y;
using OldType = Y;
typename OldType x5;
```
```

Each occurrence of typename—correct or not—is numbered with a subscript for easy reference. The first, typename, introduces a template parameter. The previous rule does not apply to this first use. The second and third occurrences are in error. They are intended to be type names. The fourth occurrence is in error. The fifth occurrence is correct because the qualified name is dependent. The sixth occurrence is in error because of condition 2: the name is part of an elaborated-type-specifier. The seventh occurrence is in error. The seventh occurrence is a lot lower than the previous rule because the template parameter is used as a type parameter. The last one of the seventh occurrence is in error because the name is dependent, but the keyword typename is required. The last one of the seventh occurrence is in error because the name is dependent, but the keyword typename is required. The last one of the seventh occurrence is in error because the name is dependent, but the keyword typename is required.