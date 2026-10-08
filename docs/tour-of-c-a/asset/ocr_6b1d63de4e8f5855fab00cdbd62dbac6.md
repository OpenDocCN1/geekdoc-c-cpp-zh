```
auto cplx = istream_view<complex<double>>(cin);

for (auto x : transform_view(cplx, [](auto z){ return z*z;}))
  cout << x << '\n';
```