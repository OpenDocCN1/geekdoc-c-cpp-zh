```
```cpp
template<typename T>
void foo(T t)
{
    if constexpr (std::is_integral_v<T>) {
        if (t > 0) {
            foo(t-1);   // OK
        }
    }
    else {
        undeclared(t);      // error if not declared and not discarded (i.e. T is not integral)
        undeclared();       // error if not declared (even if discarded)
        static_assert(false, "no integral");   // always asserts (even if discarded)
        static_assert(!std::is_integral_v<T>, "no integral");   // OK
    }
}
```
```