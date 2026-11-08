```
```cpp
template<ForwardIterator T, typename D>
void advance(T& it, D n)
{
    assert(n >= 0);
    for (; n != 0; --n) { ++it; }
}

template<BidirectionalIterator T, typename D>
void advance(T& it, D n)
{
    if (n > 0) {
        for (; n != 0; --n) { ++it; }
    } else if (n < 0) {
        for (; n != 0; ++n) { --it; }
    }
}
```
```