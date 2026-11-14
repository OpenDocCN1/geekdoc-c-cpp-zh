```
template <>
decltype(auto) get<0, int>(const complex<int>& z)
{ return z.real(); }
template <>
decltype(auto) get<1, int>(const complex<int>& z)
{ return z.imag(); }
```