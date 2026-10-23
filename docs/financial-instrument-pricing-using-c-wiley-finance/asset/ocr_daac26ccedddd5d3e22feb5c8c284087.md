```
ublas::vector<double> zarr(NZ+1, 0.0);
zarr[0] = a3;
for (std::size_t i = 1; i < zarr.size(); ++i) zarr[i] = zarr[i-1] + hz;

// Init the tensor
for (Index i = 0; i != NX+1; ++i)
{
    for (Index j = 0; j != NY+1; ++j)
    {
        for (Index k = 0; k != NZ+1; ++k)
        {
            Values[i][j][k] = 0.0;
        }
    }
}

for (Index i = 1; i != NX+1; ++i)
{
    for (Index j = 1; j != NY+1; ++j)
    {
        for (Index k = 1; k != NZ+1; ++k)
        {
            Values[i][j][k] = Values[i - 1][j][k]
                + Values[i][j - 1][k] - Values[i - 1][j - 1][k]
                + Values[i][j][k - 1] - Values[i - 1][j][k - 1]
                - Values[i][j - 1][k - 1] + Values[i - 1][j-1][k - 1]

            // Value of RHS as centre of gravity)
            + hx*hy*hz*f(xarr[i-1] + hx/2, yarr[j-1] + hy/2,
                zarr[k-1] + hz/2,
        }
    }
}

return Values[NX][NY][NZ];
}
```

```
double M(double b1, double b2, double b3,
    double a21, double a31, double a32,
    int NX, int NY, int NZ)
{ // The cumulative trivariate normal distribution at (b1,b2,b3,rho)

    double result = IntegralValues(b1,b2,b3, a21, a31, a32, NX,NY, NZ);

    return result;
}
```

An initial test case is:

```
std::cout << "Give the values of x, y and z" << std::endl;
double x, y, z;
```