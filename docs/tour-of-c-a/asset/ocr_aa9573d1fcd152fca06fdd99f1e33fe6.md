```
template<typename F, typename... Args>
auto call(F f, Args... a, Allocator alloc)
{
    if constexpr (invocable<F,alloc,Args...>) // needs an allocator?
        return f(f,alloc,a...);
    else
        return f(f,a...);
}
```