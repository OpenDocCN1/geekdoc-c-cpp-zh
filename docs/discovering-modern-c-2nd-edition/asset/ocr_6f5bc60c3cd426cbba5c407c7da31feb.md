```
```cpp
class para_sin_plus_cos
: public functor_base
{
public:
para_sin_plus_cos(double p) : alpha{p} {}

virtual double operator() (double x) const override
{
return sin(alpha * x) + cos(x);
}

private:
double alpha;
};
```
```