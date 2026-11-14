```
double d = 7.2;
unique_ptr<double> dd{&d}; // Error: causes illegal deletion
```