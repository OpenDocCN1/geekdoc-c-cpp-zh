```
```cpp
template <typename Iter, typename Value>
Value accumulate(Iter first, Iter last,
                 Value init)
requires Summable<Iter, Value>
{
    for (; first != last; ++first)
        init += *first;
    return init;
}
```
```