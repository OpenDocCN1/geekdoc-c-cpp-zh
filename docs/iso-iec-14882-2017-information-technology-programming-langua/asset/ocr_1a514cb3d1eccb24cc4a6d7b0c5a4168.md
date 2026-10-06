# ISO/IEC 14882:2017(E)

```
using result_type = bool;
};

template <class T> struct bit_and {
    using first_argument_type = T;
    using second_argument_type = T;
    using result_type = T;
};

template <class T> struct bit_or {
    using first_argument_type = T;
    using second_argument_type = T;
    using result_type = T;
};

template <class T> struct bit_xor {
    using first_argument_type = T;
    using second_argument_type = T;
    using result_type = T;
};

template <class T> struct bit_not {
    using argument_type = T;
    using result_type = T;
};

template<class R, T1> class function<R(T1)> {
public:
    using argument_type = T1;
};

template<class R, T1, T2> class function<R(T1, T2)> {
public:
    using first_argument_type = T1;
    using second_argument_type = T2;
};
```

reference_wrapper<T> has a weak result type (D.8.1). If T is a function type, result_type shall be a synonym for the return type of T.

The template reference_wrapper<T> shall define a nested type named argument_type as a synonym for T1 if the T is any of the following:

+   - a function type or a pointer to function taking one argument of type T1
- a pointer to member function T0::f(cv) (where cv represents the member function's cv-qualifiers); the type T1 is cv T0*

a class type whose qualified-id T::argument_type is valid and denotes a type (17.8.2); the type T1 is T::argument_type.

The template instantiation reference_wrapper<T> shall define two nested types first_argument_type and second_argument_type as synonyms for T1 and T2, respectively, only if the T is any of the following:

+   - a function type or a pointer to function taking two arguments of types T1 and T2
- a pointer to member function T0::f(T2) (where cv represents the member function's cv-qualifiers);