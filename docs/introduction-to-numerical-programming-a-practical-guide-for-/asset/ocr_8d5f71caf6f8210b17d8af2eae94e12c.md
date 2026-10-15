# Listing 9.9  Multilinear Regression (Python Coding)

```
```python
#==============================================================================
def MultiFit(x, y, sigmy, n, iopt, a, sigma, npar, Func):
#------------------------------------------------------------------------------
# Determines the coefficients a[i], i=1,...,npar of a multilinear model
#     F(x;a) = a[1] * func[1](x) + ... + a[npar] * func[npar](x)
# and the associated uncertainties, sigma[i], for a set of observed data
# points by "Chi-square" regression
# x[]     - x-coordinates of observed data, i = 1,...,n
# y[]     - y-coordinates of observed data
# sigmy[]  - standard deviations of observed data
# n       - number of observed data points
# iopt    - iopt == 0 - initializes sigmy[i] = 1 (equal weights)
#           iopt != 0 - uses the received values of sigmy[i]
# a[]     - parameters of the multilinear model (output)
# sigma[] - uncertainties associated with the model parameters (output)
# npar    - number of model parameters
# chi2    - value of Chi-square merit function for the output parameters
# Func()  - user function returning for a given argument x the values of the
#           basis functions func[i](x):
#               Func(x, func, npar)
# Calls: GaussJordan (linsys.py)
#==============================================================================

    c = [[0]*(n+1) for i in range(n+1)]
    b = [0]*2 for i in range(n+1)]
    func = [0]*(npar+1)

    if (iopt == 0):
        for i in range(1,n+1): sigmy[i] = 1e0       # iopt = 0: equal weights

    for i in range(1,npar+1):                                      # initialization
        for j in range(1,npar+1): c[i][j] = 0e0
        b[i][1] = 0e0

    for i in range(1,n+1):                              # generate the system matrices
        yi = y[i]
        Func(x[i],func,npar)                            # evaluate the basis functions
        f = 1e0/(sigmy[i]*sigmy[i])
        for j in range(1,npar+1):
            fj = f * func[j]
            for k in range(1,npar+1): c[j][k] += fj * func[k]
            b[j][1] += fj * yi

    det = GaussJordan(c,b,npar,1)                                  # solve the system

    for i in range(1,npar+1):
        a[i] = b[i][1]                                             # model parameters
        sigma[i] = sqrt(c[i][i])                          # parameter uncertainties

    chi2 = 0e0                                           # value of Chi-square function
    for i in range(1,n+1):
        Func(x[i],func,npar)                              # evaluate the model function
        f = 0e0
        for j in range(1,npar+1): f += a[j]*func[j]
        f = (y[i] - f)/sigmy[i]
        chi2 += f*f
    return chi2
```
```