```
if constexpr(std::is_same_v<std::invoke_result_t<Callable, Args...>, void>)
```