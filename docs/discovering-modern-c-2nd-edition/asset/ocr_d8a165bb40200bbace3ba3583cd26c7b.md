```
template <long N>
struct fibonacci
{
static const long value= fibonacci<N-1>::value
+ fibonacci<N-2>::value;
};
```

```
template <>
struct fibonacci<1>
{
static const long value= 1;
};
```

```
template <>
struct fibonacci<2>
{
static const long value= 1;
};
```