```
struct times
{
    template <typename T>
    T operator()(const T& x, const T& y) const { return x * y; }
};
```