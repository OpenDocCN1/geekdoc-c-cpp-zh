```
template <unsigned BSize, typename Value>
struct multi_tmp
{
    Value sum() const { return value + sub.sum(); }
};
```

```
template <typename Value>
struct multi_tmp<0, Value>
{
    Value sum() const { return 0; }
};
```