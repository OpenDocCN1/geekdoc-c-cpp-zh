```
col = [""]*(nmax+1)
color = ["blue", "cyan", "green", "orange", "red"]

# colors of plots

for m in range(1,nx+1): x[m] = xa + (m-1)*hx
# generate x-mesh

GraphInit(1200,600)

for n in range(1,nmax+1):
    # Legendre polynomials
    # loop over polynomial order
    alf1 = -1e0 if n % 2 else 1e0; bet1 = 0e0
    # Dirichlet conditions
    alf2 = 1e0; bet2 = 0e0
    Bilocal(xa,xb,y,nx,alf1,bet1,alf2,bet2,Func)

    nn[n] = n*nx; col[n] = color[(n-1)%5]; sty[n] = 1
    m0 = (n-1)*nx
    for m in range(1,nx+1): xp[m0+m] = x[m]; yp[m0+m] = y[m]

MultiPlot(xp,yp,yp,nn,col,sty,nmax,10,0e0,0e0,0,-1e0,1e0,1, \
    0.10,0.45,0.15,0.85,"x","Pn", \
    "Legendre polynomials - finite-differences")

for n in range(1,nmax+1):
    # Chebyshev polynomials
    # loop over polynomial order
    alf1 = -1e0 if n % 2 else 1e0; bet1 = 0e0
    # Dirichlet conditions
    alf2 = 1e0; bet2 = 0e0
    Bilocal(xa,xb,y,nx,alf1,bet1,alf2,bet2,Func1)

    nn[n] = n*nx; col[n] = color[(n-1)%5]; sty[n] = 1
    m0 = (n-1)*nx
    for m in range(1,nx+1): xp[m0+m] = x[m]; yp[m0+m] = y[m]

MultiPlot(xp,yp,yp,nn,col,sty,nmax,10,0e0,0e0,0,-1e0,1e0,1, \
    0.60,0.95,0.15,0.85,"x","Tn", \
    "Chebyshev polynomials - finite-differences")

MainLoop()
```

![](bbox=[0.13, 0.62, 0.83, 0.88])

FIGURE 12.22 Legendre polynomials P_n(x) (left) and Chebyshev polynomials of the first kind T_n(x) (right) for n = 1–5, calculated by the finite-difference method (for Problem 12.14).