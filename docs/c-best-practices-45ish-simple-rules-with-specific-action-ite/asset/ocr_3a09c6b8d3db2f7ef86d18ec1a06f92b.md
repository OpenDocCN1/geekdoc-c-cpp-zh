Prefer auto in Many Cases.

C++11 trailing return types.

```
// use trailing return type
template<typename Numerator, typename Denominator>
auto divide(Numerator numerator, Denominator denominator)
-> decltype(numerator / denominator)
{
  return numerator / denominator;
}
```

But in C++14, we can leave off the return type altogether (remember to Skip C++11).

C++14 auto return types.

```
template<typename Numerator, typename Denominator>
auto divide(Numerator numerator, Denominator denominator)
{
  return numerator / denominator;
}
```