```
template <typename T>
struct inequality
{
    bool operator!=(const T& that) const
    { return !(static_cast<const T&>(*this) == that); }
};
```