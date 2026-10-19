# ISO/IEC 14882:2020(E)

```
D d1 = {1, 2};                         // error: deduction failed
D d2 = {1, 2, 3};                       // OK, braces elided, deduces D<int>

template <typename T>
struct E {
    T t;
    decltype(t) t2;
};

E e1 = {1, 2};                          // OK, deduces E<int>

template <typename... T>
struct Types {};

template <typename... T>
struct F : Types<T...>, T... {};

struct X {};
struct Y {};
struct Z {};
struct W { operator Y(); };

F f1 = {Types<X, Y, Z>{}, {}, {}};       // OK, F<X, Y, Z> deduced
F f2 = {Types<X, Y, Z>{}, X{}, Y{}};     // OK, F<X, Y, Z> deduced
F f3 = {Types<X, Y, Z>{}, X{}, W{}};     // error: conflicting types deduced; operator Y not considered
--- end example]

6 [Example 2:
    template <class T, class U> struct C {
        C(T, U);                         // #1
    };
    template<class T, class U>
        C(T, U) -> C<T, std::type_identity_t<U>>;   // #2

template<class V> using A = C<V *, V *>;
template<std::integral W> using B = A<W>;

int i{};
double d{};
A a1(&i, &i);      // deduces A<int>
A a2(i, i);        // error: cannot deduce V * from i
A a3(&i, &d);      // error: #1: cannot deduce (V*, V*) from (int *, double *)
                   // #2: cannot deduce A<V> from C<int *, double *>
B b1(&i, &i);      // deduces B<int>
B b2(&d, &d);      // error: cannot deduce B<W> from C<double *, double *>

Possible exposition-only implementation of the above procedure:
    // The following concept ensures a specialization of A is deduced.
    template <class> class AA;
    template <class V> class AA<A<V>> { };
    template <class T> concept deduces_A = requires { sizeof(AA<T>); };

    // f1 is formed from the constructor #1 of C, generating the following function template
    template<T, U>
        auto f1(T, U) -> C<T, U>;

    // Deducing arguments for C<T, U> from C<V *, V*> deduces T as V * and U as V *;
    // f1' is obtained by transforming f1 as described by the above procedure.
    template<class V> requires deduces_A<C<V *, V *>>
        auto f1_prime(V *, V*) -> C<V *, V *>;

    // f2 is formed from the deduction-guide #2 of C
    template<class T, class U> auto f2(T, U) -> C<T, std::type_identity_t<U>>;
```