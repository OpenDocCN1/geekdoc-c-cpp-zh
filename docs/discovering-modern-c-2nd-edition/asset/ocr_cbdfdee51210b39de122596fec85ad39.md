```
optional<double> square_root(double x)
{
    if (x < 0.0)
        return nullopt;
    else
        return sqrt(x);
}
```