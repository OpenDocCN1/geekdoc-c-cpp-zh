We stress that only labelled rows are displayed in the current version of the software. In most cases, we would ensure that the number of labels should be the same as the corresponding matrix dimensions in order to view all the data. We thus see that not all rows from Figure 14.1 are visible in Figure 14.2. You need to be aware of this fact.

# 14.4.3 Lookup Tables, Continuous and Discrete Functions

A common use case is when we discretise real-valued functions of arity one and two. Focusing on the latter case we create two discrete mesh arrays and we compute the value of a function at these points. These values will be the values in the matrix. As an example, we discretise the bivariate normal probability density function defined in the following way for convenience (the correlation variable is global):

```
double rho = 0.5;
double NormalPdf2d(double x, double y)
{ // Bivariate normal density function

double fac= 1.0/(2.0 * 3.14159265359 * std::sqrt(1.0 - rho*rho));
double t = x*x - 2.0*rho*x*y + y*y;
t /= 2.0 * (1.0 - rho*rho);

return fac * std::exp(-t);
}
```

In order to discretise this function, we use the following utility function:

```
template <typename Matrix>
Matrix CreateDiscreteFunction2d(const std::vector<double>& x ,
const std::vector<double>& y,
const std::function<double (double x, double y)>& f)
{ // Create a discrete function from a continuous function m = f(x,y)

std::size_t nr = x.size();
std::size_t nc = y.size();

Matrix m(nr,nc);

for (std::size_t i = 0; i < nr; ++i)
{
for (std::size_t j = 0; j < nc; ++j)
{
m(i, j) = f(x[i],y[j]);
}
}

return m;
}
```

This code can be parallelised, as discussed in Chapters 28 to 30.