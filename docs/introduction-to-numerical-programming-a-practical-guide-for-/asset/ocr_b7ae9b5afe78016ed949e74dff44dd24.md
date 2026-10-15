# Listing 5.15 Exponential Function from Its Continued Fraction Representation (Python Coding)

```
#===============================================================================
def Exp1(x):
#-------------------------------------------------------------------------------
# Evaluates exp(x) from its continued fraction representation
#-------------------------------------------------------------------------------
eps = 1e-14                                      # relative precision

a = 1e0; b = x
pm1 = 1e0; p = 1e0 + x
qm1 = 1e0; q = 1e0
rm1 = 1e0; r = p/q
i = 1
while (fabs(r-rm1) > eps*fabs(r)):
    i += 1
    pm2 = pm1; pm1 = p                         # shift the stack
    qm2 = qm1; qm1 = q
    rm1 = r
    a = (i if i%2 else 2e0)
    b = -b
    p = a*pm1 + b*pm2
    q = a*qm1 + b*qm2
    r = (p/q if q else 9e99)                   # new convergent value

return r
```

The following starting values can be used:

⎧ a₁ = 1,   b₁ = x,
  P₀ = 1,   P₁ = 1 + x,
  Q₀ = 1,   Q₁ = 1.   (5.67)

The recursive evaluation of the convergents Rᵢ can be carried out based on the relations:

⎧ aᵢ = { 2,  i = 2,4,…,
          i,  i = 3,5,…,
     bᵢ = −bᵢ₋₁,   (5.68)

and

⎧ Pᵢ = aᵢPᵢ₋₁ + bᵢPᵢ₋₂,
  Qᵢ = aᵢQᵢ₋₁ + bᵢQᵢ₋₂,
  Rᵢ = Pᵢ/Qᵢ.   (5.69)

The Python implementation of the routine is given in Listing 5.15, being included in the module elemfunc.py, and the corresponding C/C++ variant is part of the header file elemfunc.h.

# PROBLEM 5.4

Write a program to calculate the squared norms |Yₗᵐ(θ,φ)|² of the spherical harmonics (defined by Equation 5.35), for l = 0,1,2 and m = −l,−l+1,…,l, using the function SpherY from the modules