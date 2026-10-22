```
template<typename Coll, typename... T>
void insert(Coll& coll, T&&... val)
{
    if constexpr(!std::is_aggregate_v<typename Coll::value_type>) {
        coll.emplace_back(std::forward<T>(val)...);  // invalid for aggregates
    }
    else {
        coll.emplace_back(typename Coll::value_type{std::forward<T>(val)...});
    }
}
```