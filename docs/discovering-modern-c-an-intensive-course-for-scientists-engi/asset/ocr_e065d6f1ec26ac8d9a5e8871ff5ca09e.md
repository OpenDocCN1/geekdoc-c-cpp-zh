# 3.9.3 Capture by Reference

Variables can also be captured by reference:

```
```cpp
double phi = 2.5, xi = 0.2;
auto pxr = [&phi, &xi](double x){ return sin(phi * x) + cos(x) * xi; };
phi = 3.5; xi = 1.2;
a = fin_diff(pxr, 1., 0.001); // now uses phi = 3.5 and xi = 1.2
```
```

In this example, the values of phi and xi at the time of the function call of \(\Lambda\) are used—not those when the lambda was created. The corresponding functor class would look like this:

```
```cpp
struct lambda_ref_type
struct lambda_f
{
    lambda_ref_type(double& phi, double& xi) : phi(phi), xi(xi) {}
    double operator()(double x)
    {
        return sin(phi * x) + cos(x) * xi;
    }
    double& phi;
    double& xi;
};
```
```

Another consequence of the reference semantics is the ability to modify the referred values. This is not only a possible source of side effects but can be used productively. Let's say we have different dense and sparse matrix classes. For all those classes, we provide the generic traversal function on_each_nonzero with the matrix as the first argument and a function object as the second (passed by value). This allows us to generically compute the Frobenius norm:

![](bbox=[0.38, 0.6, 0.6, 0.64])

Given this formula, we can apparently ignore all zero entries and process the non-zeros only:

```
```cpp
template <typename Matrix>
typename Matrix::value_type
frobenius_norm(const Matrix& A)
{
    using std::abs; using std::sqrt;
    using value_type = typename Matrix::value_type;
    value_type ss = 0;
    on_each_nonzero(A, [&&](value_type x) { ss += abs(x) * abs(x); });
    return sqrt(ss);
}
```
```

For simplicity's sake, we assume here that the types of A(0,0) and abs(A(0,0)) are identical. Note that the \(\lambda\)-expression doesn't return a value since its purpose is to sum up the squared matrix values in the referred variable ss. Here the lack of a return statement implies the void return type.