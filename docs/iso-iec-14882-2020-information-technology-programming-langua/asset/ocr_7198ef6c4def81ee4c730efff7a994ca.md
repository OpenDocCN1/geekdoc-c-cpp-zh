— If there is such a type C, the member typedef type shall denote the same type, if any, as common_reference_t<C, Rest...>.

— Otherwise, there shall be no member type.

Note D: Notwithstanding the provisions of 20.15.3, and pursuant to 16.4.5.2.1, a program may partially specialize basic_common_reference<T, U, TQual, UQual> for types T and U such that is_same_v<T, decay_t<T>> and is_same_v<U, decay_t<U>> are each true.

> [*Note 6:* Such specializations can be used to influence the result of `common_reference`, and are needed when only explicit conversions are desired between the template arguments. — *end note*]

Such a specialization need not have a member named `type`, but if it does, that member shall be a *typedef-name* for an accessible and unambiguous type C to which each of the types TQual<T> and UQual<U> is convertible. Moreover, basic_common_reference<T, U, TQual, UQual>::type shall denote the same type, if any, as does basic_common_reference<U, T, UQual, TQual>::type. No diagnostic is required for a violation of these rules.

> [*Example 2:* Given these definitions:]

```
using PF1 = bool    (S&)();
using PF2 = short  (*)(long);

struct S {
  operator PF2() const;
  double operator()(char, int&) ;
  void fn(long) const;
  char data;
};

using PMF = void (S::*)(long) const;
using PMD = char  S::*;
```

the following assertions will hold:

```
static_assert(is_same_v<invoke_result_t<S, int>, short>);
static_assert(is_same_v<invoke_result_t<S&, unsigned char, int&>, double>);
static_assert(is_same_v<invoke_result_t<PF1>, bool>);
static_assert(is_same_v<invoke_result_t<PMF, unique_ptr<S>, int>, void>);
static_assert(is_same_v<invoke_result_t<PMD, S>, char&&>);
static_assert(is_same_v<invoke_result_t<PMD, const S*>, const char&>);
```

> — *end example*

# 20.15.9  Logical operator traits

This subclause describes type traits for applying logical operators to other type traits.

```
template<class... B> struct conjunction : see below { };
```

The class template `conjunction` forms the logical conjunction of its template type arguments.

For a specialization `conjunction<B₁, ..., Bₙ>`, if there is a template type argument Bᵢ for which `bool(Bᵢ::value)` is false, then instantiating `conjunction<B₁, ..., Bₙ>::value` does not require the instantiation of `Bⱼ::value` for j > i.

> [*Note 1:* This is analogous to the short-circuiting behavior of the built-in operator `&&`. — *end note*]

Every template type argument for which Bᵢ::value is instantiated shall be usable as a base class and shall have a member value which is convertible to bool, is not hidden, and is unambiguously available in the type.

The specialization `conjunction<B₁, ..., Bₙ>` has a public and unambiguous base that is either

+   1. the first type Bᵢ in the list `true_type, B₁, ..., Bₙ` for which `bool(Bᵢ::value)` is false, or
+   2. if there is no such Bᵢ, the last type in the list.

> [*Note 2:* This means a specialization of `conjunction` does not necessarily inherit from either `true_type` or `false_type`. — *end note*]

The member names of the base class, other than `conjunction` and `operator=`, shall not be hidden and shall be unambiguously available in `conjunction`.