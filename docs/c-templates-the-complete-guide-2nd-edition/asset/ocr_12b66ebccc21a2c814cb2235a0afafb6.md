Section C.2.1 on page 684) and, since C++17, noexcept qualifiers. For example: Click here to view code image

```
using MyFuncType = void (int&) const; Such function types can only be meaningfully used for nonstatic member functions but are function types nonetheless. Moreover, a function type marked const is not actually a const type,27 so RemoveConst is not able to strip the const from the function type. Therefore, to recognize function types that have qualifiers, we need to introduce a large number of additional partial specializations, covering every combination of qualifiers (both with and without C-style varargs). Here, we illustrate only five of the many28 required partial specializations: Click here to view code image
```

```
template<typename R, typename... Params>
struct IsFunctionT<R (Params...) const> : std::true_type {
using Type = R;
using ParamsT = Typelist<Params...>; 
static constexpr bool variadic = false;
};
```

```
template<typename R, typename... Params>
struct IsFunctionT<R (Params..., ...) volatile> : std::true_type {
using Type = R;
using ParamsT = Typelist<Params...>; 
static constexpr bool variadic = true;
};
```

```
template<typename R, typename... Params>
struct IsFunctionT<R (Params..., ...) const volatile> : std::true_type {
using Type = R;
using ParamsT = Typelist<Params...>; 
static constexpr bool variadic = true;
};
```

```
template<typename R, typename... Params>
struct IsFunctionT<R (Params..., ...) &> : std::true_type {
using Type = R;
using ParamsT = Typelist<Params...>; 
static constexpr bool variadic = true;
};
```

```
template<typename R, typename... Params>
struct IsFunctionT<R (Params..., ...) const&> : std::true_type {
using Type = R;
using ParamsT = Typelist<Params...>; 
static constexpr bool variadic = true;
};
...
```

With all this in place, we can now classify all types except class types and