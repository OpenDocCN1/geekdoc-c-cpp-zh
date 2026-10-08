```
template<class... Ts>
struct overloaded : Ts... { // variadic template ($8.4)
    using Ts::operator()...;
};
```

```
template<class... Ts>
    overloaded(Ts...) -> overloaded<Ts...>; // deduction guide
```