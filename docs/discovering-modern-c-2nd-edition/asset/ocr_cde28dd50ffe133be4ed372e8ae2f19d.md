```
struct lambda_ref_type
{
    lambda_ref_type(double& phi, double& xi) : phi{phi}, xi{xi} {}
    double operator()(double x) const
    {
        return sin(phi * x) + cos(x) * xi;
    }
    double& phi;
    double& xi;
};
```