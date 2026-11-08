block scope.

So far, this technique might seem compelling because both the expressions involved in the implementation and the style of use are more complex than the previous techniques. However, once a `yield` is placed in place and understood, many traits can be implemented with just one declaration. For example, testing for access to a member named `first` is rather clean (see Section 19.6.1 on page 438 for the complete example):

[Click here to view code image](#)

```
template<typename T>
struct HasFirst {
  template<typename U>
  static auto test(U* u) -> decltype(u->first);
};
```

# 19.9.4 SFINAE-Friendly Traits

In general, a type trait should be able to answer a particular query without causing the program to become ill-formed. SFINAE-based traits address this problem by carefully trapping potential problems within a SFINAE context, turning those would-be errors into negative results.

However, some traits presented thus far (such as the `PlusResultT` trait described in Section 19.3.4 on page 434) do not behave well in the presence of errors. Recall the definition of `PlusResultT<>` from that section:

[Click here to view code image](#)

```
template<typename T1, typename T2>
struct PlusResult {
  using Type = decltype(std::declval<T1>() + std::declval<T2>());
};

template<typename T1, typename T2>
using PlusResultT = typename PlusResult<T1, T2>::Type;
```

In this definition, the `+` is used in a context that is not protected by SFINAE. Therefore, if a program attempts to evaluate `PlusResult<T>` for types that do not have a suitable `+` operator, that evaluation of `PlusResult<T>` itself will cause the program to become ill-formed, as in the following attempt to declare the return type of adding arrays of unrelated types `A` and `B`:

[Click here to view code image](#)

```
template<typename T>
class Array {
};

template<typename T1, typename T2>
Array<PlusResultT<T1, T2>>
operator+(Array<T1> const&, Array<T2> const&);
```

Clearly, using `PlusResultT<>` here will lead to an error if no corresponding operator `+` is defined for the array element.

[Click here to view code image](#)

```
class A {
};

class B {
};

void add(Array<A> const&, Array<A> const&);

// declare a + for arrays of different element types:
template<typename T1, typename T2>
Array<PlusResultT<T1, T2>>
operator+(Array<T1> const&, Array<T2> const&);
```