```
r = b - ublas::prod(A,x);
ublas::vector<double> p(r);

double a;
double beta;
double norm, norm2;
ublas::vector<double> tmpVec(n);

for (size_t j=1; j<=n; ++j)
{
    // Step 1.
    norm = ublas::norm_2(r);
    norm *= norm;

    // Exit loop is convergence has been reached.
    if (norm <= tol) break;

    tmpVec = ublas::prod(A, p);
    a = norm / ublas::inner_prod(p, tmpVec);

    // Step 2.
    x += a*p;

    // Step 3.
    r -= a*tmpVec;

    // Step 4.
    norm2 = ublas::norm_2(r); norm2 *= norm2;
    beta = norm2 / norm;
    p = beta*p + r;
}
```

The CGM algorithm in the case of a general matrix A is:

r₀ = F − AU₀
p₀ = r₀

for j = 1, 2, ..., n:

aⱼ = ||Aᵀ rⱼ||² / ||A pⱼ||²
Uⱼ₊₁ = Uⱼ + aⱼ pⱼ
rⱼ₊₁ = rⱼ − aⱼ A pⱼ
bⱼ = ||Aᵀ rⱼ₊₁||² / ||Aᵀ rⱼ||²
pⱼ₊₁ = Aᵀ rⱼ₊₁ + bⱼ pⱼ.

We leave it as an exercise to modify the CGM code for symmetric matrices so that it works in the case (non-symmetric) just given.