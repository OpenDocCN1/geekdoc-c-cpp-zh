```
Pair(Pair&& other) noexcept(IsNothrowMoveConstructibleT<T1>::value &&
    IsNothrowMoveConstructibleT<T2>::value)
  : first(std::forward<T1>(other.first)),
    second(std::forward<T2>(other.second))
{
}
```