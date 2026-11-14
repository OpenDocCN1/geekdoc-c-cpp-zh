```
template <typename Iter, typename Value>
requires Summable<Iter, Value>
Value accumulate(Iter first, Iter last, Value init);
```