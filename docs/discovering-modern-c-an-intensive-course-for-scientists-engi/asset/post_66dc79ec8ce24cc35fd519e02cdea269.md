
```
vector_bool_proxy& operator=(bool b)
{
    if (b)
        byte|= mask;
    else
        byte&= ~mask;
    return *this;
};
```

The assignment is simpler to implement when we distinguish between the assigned values.
When the argument is true, we apply an OR with the mask so that the bit in the considered position is switched on. All other positions remain unchanged since OR with 0 has no effect (0 is the identity element of bitwise OR). Conversely, with false as an argument, we first invert the mask and apply it with AND to the byte reference. Then the mask's zero bit on the active position turns the bit off. On all other positions, the AND with one bit conserves the old bit values.

With this specialization of vector for bool, we only use about an eighth of the memory.
Nonetheless, this specialization is (mostly) consistent with the primary template: we can create vectors and read and write them in the same fashion. To be honest, the compressed vector is not perfectly identical to the primary template, e.g., when we take references of elements or when type deduction is involved. However, we made the specialization as similar as possible to the generic version and in most situations we will not realize the differences and it will work in the same way.

## 3.6.2 Specializing and Overloading Functions

In this section, we discuss and assess the advantages and disadvantages of template specialization for functions.

### 3.6.2.1 Specializing a Function to a Specific Type

Functions can be specialized in the same manner as classes. Unfortunately, they do not participate in overload resolution, and a less specific overload is prioritized over the more specific template specialization; see [44]. For that reason Sutter and Alexandrescu give in [45, Item 66] the following:

### Advice

Do not use function template specialization!

To provide a special implementation for one specific type or type tuple as above, we can simply use overloading. This works better and is even simpler, e.g.:

```
#include <cmath>

template <typename Base, typename Exponent>
Base inline power(const Base& x, const Exponent& y) { ... }

double inline power(double x, double y)
{
    return std::pow(x, y);
}
```

Functions with many specializations are best implemented by means of class specialization. This allows for full and partial specialization without taking all overloading and ADL rules into consideration. We will show this in Section 3.6.4.

If you ever feel tempted to write hardware-specific specializations in assembler code, try to resist. If you cannot, please read first the few remarks in Appendix A.6.3.

### 3.6.2 Ambiguities

In the previous examples, we specialized all parameters of the function. It is also possible to specialize some of them in overloads and leave the remaining parameter(s) as template(s):

```
template <typename Base, typename Exponent>
Base inline power(const Base& x, const Exponent& y);

template <typename Base>
Base inline power(const Base& x, int y);

template <typename Exponent>
double inline power(double x, const Exponent& y);
```

The compiler will find all overloads that match the argument combination and select the most specific, which is supposed to provide the most efficient special-case implementation. For instance, power(3.0, 2u) will match for the first and third overload where the latter is more specific. To put it in terms of higher math:10 type specificity is a partial order that forms a lattice, and the compiler picks the maximum of the available overloads. However, you do not need to dive deeply into algebra to see which type or type combination is more specific.

If we called power(3.0, 2) with the previous overloads, all three would match. However, this time we cannot determine the most specific overload. The compiler will tell us that the call is ambiguous and show us overloads 2 and 3 as candidates. As we implemented the overloads consistently and with optimal performance we might be happy with either choice but the compiler will not choose. To disambiguate, we must add a fourth overload:

```
double inline power(double x, int y);
```

The lattice experts will immediately say: “Of course, we were missing the join in the specificity lattice.” But even without this expertise, most of us understand why the call was ambiguous with the three overloads and why the fourth one rescued us. In fact, the majority of C++ programmers get along without studying lattices.

10. For those who like higher mathematics. And only for those.

## 3.6.3 Partial Specialization

When we implement template classes, we will sooner or later run into situations where we want to specialize a template class for another template class. Suppose we have a template complex and vector and want to specialize the latter for all instances of complex. It would be quite annoying doing this one by one:

```
template <>
class vector<complex<float> >;
```

```
template <>
class vector<complex<double> >; // again ??? :-/
```

```
template <>
class vector<complex<long double> >; // how many more ??? :-P
```

This is not only inelegant, it also destroys our ideal of universal applicability because the complex class supports all real types and our specialization above only takes a limited number thereof into account. In particular, instances of complex with future user types cannot be considered for obvious reasons.

The solution that avoids the implementation redundancy and the ignorance of new types is Partial Specialization. We specialize our vector class for all complex instantiations:

```
template <typename Real>
class vector<complex<Real> >
{ ... };
```

If you use a compiler without C++11 support, pay attention to put spaces between closing >; otherwise your compiler may interpret two subsequent > as shift operator >>, leading to rather confusing errors. Although this book mainly addresses C++11 programming, we still keep the separating spaces for readability.

Partial specialization also works for classes with multiple parameters, for instance:

```
template <typename Value, typename Parameters>
class vector<sparse_matrix<Value, Parameters> >
{ ... };
```

We can also specialize for all pointers:

```
template <typename T>
class vector<T*>
{ ... };
```

Whenever the set of types is expressible by a Type Pattern, we can apply partial specialization on it.

Partial template specialization can be combined with regular template specialization from §3.6.1—let us call it Full Specialization for distinction. In this case, the full specialization is prioritized over the partial one. Between different partial specializations the most specific is selected. In the following example:

```
template <typename Value, typename Parameters>
class vector<sparse_matrix<Value, Parameters> >
{ ... };
```

```
template <typename Parameters>
class vector<sparse_matrix<float, Parameters> > { ... };
```

the second specialization is more specific than the first one and picked when it matches. In fact, a full specialization is always more specific than any partial one.

## 3.6.4 Partially Specializing Functions

Function templates actually cannot be specialized partially. We can, however, as for the full specialization (§3.6.2.1), use overloading to provide special implementations. For that purpose, we write more specific function templates that are prioritized when they match. As an example, we overload the generic abs with an implementation for all complex instances:

```
template <typename T>
inline T abs(const T& x)
{
    return x < T(0) ? -x : x;
}
```

```
template <typename T>
inline T abs(const std::complex<T>& x)
{
    return sqrt(real(x)*real(x) + imag(x)*imag(x));
}
```

Overloading of function templates is easy to implement and works reasonably well. However, for massively overloaded functions or for overloads spread over many files of a large project, sometimes the intended overload is not called. The reason is the non-trivial interplay of the already challenging namespace resolution with the overload resolution of mixed template and non-template functions.

```
=> c++14/abs_function.cpp
```

To ascertain a predictable specialization behavior, it is safest to implement it internally in terms of class template specialization and only provide a single function template as a user interface. The challenging part here is the return type of this single function when the return types for the specializations vary. As in our abs example: the general code returns the argument type while the more specific complex version returns the underlying value type. This can be handled in a portable way so that it works even with C++03. The newer standards, however, provide features to simplify this task.

We start with the easiest implementation by using C++14:

```
template <typename T> struct abs_functor;

template <typename T>
decltype(auto) abs(const T& x)
{
    return abs_functor<T>()(x);
}
```
