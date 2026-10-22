```
template<typename T>
struct isNoPtrT : std::negation<std::disjunction<std::is_null_pointer<T>,
    std::is_member_pointer<T>,
    std::is_pointer<T>>>
{
};
```