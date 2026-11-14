```
auto f = [] (double x) { return 2.0 * std::cos(x) + x*x; };
auto d2f = derive<2>(f, 1e-3);
auto d5f = derive<5>(f, 1e-3);
```

```
cout << "f''(1) = " << d2f(1.0) << endl;
cout << "f(5)(1) = " << d5f(1.0) << endl;
```