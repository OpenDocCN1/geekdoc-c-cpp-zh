```
fm2 = fm1; fm1 = f;
    f = ((2*i-1)*x*fm1 - (i-1)*fm2)/i;
}
    d = (x*x-1e0) ? n*(x*f-fm1)/(x*x-1e0) : 0.5*n*(n+1)*f/x;
}
    return f;
}

//================================================================================
double aLegendre(int l, int m, double x)
//--------------------------------------------------------------------------------
// Evaluates the associated Legendre function of orders l and m >= 0 in x
//--------------------------------------------------------------------------------
{
    double p, pm1, pm2, sqx;
    int i;

    if (l < m) return 0e0;

    p = 1e0; pm1 = 0e0;                     // seed values: P(m,m,x), P(m-1,m,x)
    if (m) {
        sqx = -sqrt(1e0-x*x);
        for (i=1; i<=m; i++) p *= (2*i-1) * sqx;
    }

    for (i=m+1; i<=l; i++) {                 // recurrence
        pm2 = pm1; pm1 = p;
        p = ((2*i-1)*x*pm1 - (i+m-1)*pm2)/(i-m);
    }
    return p;
}

//================================================================================
double Laguerre(int n, double x, double &d)
//--------------------------------------------------------------------------------
// Evaluates the n-th order Laguerre polynomial and its derivative d in x
// using the recurrence relation
//--------------------------------------------------------------------------------
{
    double f, fm1, fm2;
    int i;

    if (n == 0) {
        f = 1e0; d = 0e0;
    } else {
        f = 1e0 - x; fm1 = 1e0;
        for (i=2; i<=n; i++) {
            fm2 = fm1; fm1 = f;
            f = ((2*i-1-x)*fm1 - (i-1)*fm2)/i;
        }
        d = x ? n*(f-fm1)/x : -n*f;
    }
    return f;
}

//================================================================================
double aLaguerre(int n, int k, double x)
//--------------------------------------------------------------------------------
// Evaluates the associated Laguerre polynomial of orders n and k in x
```