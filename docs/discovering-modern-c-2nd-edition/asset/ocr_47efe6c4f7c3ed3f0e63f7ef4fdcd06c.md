```
template <typename Op, typename Value>
concept SemiGroup =
    Magma<Op, Value> &&
    semi_group_map<Op, Value>;
```