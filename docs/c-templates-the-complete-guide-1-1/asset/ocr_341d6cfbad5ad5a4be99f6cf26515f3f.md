the type of the class in which that member occurs.

The C++ standard library provides more specific traits, `std::is_member_object_pointer<T>` and `std::is_member_function_pointer<T>`, which are described in Section 2.1.1 on page 75, as well as `std::is_member_pointer<T>`, which is described in Section 3.2.2 on page 76.

# ### 9.8.3 Identifying Function Types

Function types are interesting because they have an arbitrary number of parameters in addition to the return type. Therefore, within the partial specialization matching a function type, we employ a parameter pack to capture all of the parameter types, as we did for the `Decay` trait in Section 10.3.2 on page 149.

**Click here to view code image**

```
```cpp
template<typename T>
struct IsFunctionT : std::false_type { /*primary
                                      template*/
};

template<typename R, typename... Params>
struct IsFunctionT<R(Params...)> : std::true_type {
  using Type = R;
  using ParamT = TypeList<Params...>;
  static constexpr bool value = false;
};

template<typename R, typename... Params>
struct IsFunctionT<R(Params...) &> : std::true_type {
  using Type = R;
  using ParamT = TypeList<Params...>;
  static constexpr bool value = true;
};
```
```

Notice that each part of the function type is expressed: The return type is the result type, while all of the parameters are captured in a single typelist as `ParamT` (typelists are covered in Chapter 4), and variadic indirection rather than the function type uses C-style varargs.

Unfortunately, this formulation of `IsFunctionT` does not handle all function types, because function types can have const and volatile qualifiers as well as a value (`&`) and rvalue (`&&`) reference qualifiers (described in Section 2.1.1 on page 63), and since C++17, `noexcept` qualifiers. For example:

**Click here to view code image**

```
```cpp
using MyFunction = void(int) const;

Such function types can only be meaningfully used for nonstatic member
functions that are function types themselves. Moreover, a function type
member must consist of an exact arbitrary const type? To demonstrate, it is not able
to strip the const from the function type. Therefore, to recognize function
types that have qualifiers, we need to introduce a large number of addi-
tional partial specializations, covering every combination of qualifiers
(both lvalue and rvalue). Here, we illustrate only a few of
the many qualified partial specializations:

template<typename R, typename... Params>
struct IsFunctionT<R(Params...) const> : std::true_type {
  using Type = R;
  using ParamT = TypeList<Params...>;
  static constexpr bool value = false;
};

template<typename R, typename... Params>
struct IsFunctionT<R(Params...) volatile>
  : std::true_type {
  using Type = R;
  using ParamT = TypeList<Params...>;
  static constexpr bool value = true;
};

template<typename R, typename... Params>
struct IsFunctionT<R(Params...) const volatile>
  : std::true_type {
  using Type = R;
  using ParamT = TypeList<Params...>;
  static constexpr bool value = true;
};
```
```