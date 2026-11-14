```
template <bool Condition, typename ThenType, typename ElseType>
struct conditional
{
    using type = ThenType;
};

template <typename ThenType, typename ElseType>
struct conditional<false, ThenType, ElseType>
{
    using type = ElseType;
};
```