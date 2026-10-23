```
return y;
}

template <typename Matrix>
Matrix CreateDiscreteFunction2d(const std::vector<double>& x ,
    const std::vector<double>& y,
    const std::function
        <double (double x, double y)>& f)
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

# 14.6 PATH GENERATION FOR STOCHASTIC DIFFERENTIAL EQUATIONS

The generic examples in the preceding sections were chosen to show how the Excel driver works without becoming embroiled in software design decisions or mathematically advanced discussions. In this section we take examples that are related to computational finance. To this end, we simulate the paths of quantities that are defined by SDEs. In most cases analytical solutions do not exist and we must resort to numerical approximations, in this case the finite difference method.

We now discuss some schemes to calculate the path of the following nonlinear autonomous SDE:

dX(t) = μ(X(t))dt + σ(X(t))dW(t)    0 < t ≤ T
X(0) = A.                                    (14.1)

Some finite difference schemes are:

+   - Explicit Euler:
+   
+     Xₙ₊₁ = Xₙ + μₙΔt + σₙΔWₙ
+     where:
+     μₙ = μ(Xₙ)  σₙ = σ(Xₙ).                                    (14.2)