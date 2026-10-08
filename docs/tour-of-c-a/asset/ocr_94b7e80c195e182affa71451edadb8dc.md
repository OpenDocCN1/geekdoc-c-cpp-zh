```
template<typename T>
void update(T& target)
{
    // ...
    if constexpr(is_trivially_copyable_v<T>)
        simple_and_fast(target); // Il for "plain old data"
    else
        slow_and_safe(target); // Il for more complex types
    // ...
}
```