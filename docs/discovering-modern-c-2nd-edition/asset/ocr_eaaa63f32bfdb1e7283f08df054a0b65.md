```
struct functor_base
{
    virtual double operator() (double x) const= 0;
    virtual ~functor_base() = default;
};
```