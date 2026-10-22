```
template<typename... Types> class Tuple {
};

template<typename T, typename... Types>
struct Split;

template<typename T, typename... Before, typename... After>
struct Split<T, Before..., T, After...> {
    using before = Tuple<Before...>;
    using after = Tuple<After...>;
};
```