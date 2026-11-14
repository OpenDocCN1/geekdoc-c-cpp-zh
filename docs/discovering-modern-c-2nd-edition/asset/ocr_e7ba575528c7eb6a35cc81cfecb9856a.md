```
template <typename Value>
struct vec
{
    vec(unsigned s) : s(s), d(new Value[s]) {}
};

vec x(3);
```