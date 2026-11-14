```
```cpp
struct simple_point
{
# ifdef __cplusplus
simple_point(double x, double y) : x(x), y(y) {}
simple_point() = default;
simple_point(initializer_list<double> il)
{
    auto it= begin(il);
    x= *it;
    y= *next(it);
}
# endif
double x, y;
};
```
```