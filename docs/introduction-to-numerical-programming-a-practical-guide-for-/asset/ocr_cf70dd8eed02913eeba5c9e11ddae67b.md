```
t += ht; it += 1

if (u[1]*us < 0e0):                 # count solution passages through zero
    if (t1 == 0): t1 = t             # initial zero
    else: t2 = t; nT += 1            # final zero
us = u[1]                            # save solution
                                      # store for plotting
if (iu == 1): tt[it    ] = t; ut[it    ] = u[1]       # for smallest u0
if (iu == nu): tt[it+nt] = t; ut[it+nt] = u[1]       # for largest u0

T = 2e0*(t2-t1) / nT                 # calculated period
T0 = 2*pi*sqrt(1/g)                   # harmonic period
Tex = 2/pi * T0 * Kel(pow(sin(0.5e0*u0),2))           # exact period

uu[iu    ] = u0; tu[iu    ] = T/T0
uu[iu+nu] = u0; tu[iu+nu] = Tex/T0

GraphInit(1200,600)

nn[1] = it    ; col[1] = "blue"; sty[1] = 1          # for smallest u0
nn[2] = it+nt ; col[2] = "red" ; sty[2] = 1          # for largest u0
MultiPlot(tt,ut,ut,nn,col,sty,2,10,0e0,0e0,0,0e0,0e0,0,0.10,0.45,0.15,0.85, \
          "t (s)","u (rad)","Displacement of nonlinear pendulum")

nn[1] = nu; col[1] = "red" ; sty[1] = 0                # calculated periods
nn[2] = 2*nu; col[2] = "blue"; sty[2] = 1             # exact periods
MultiPlot(uu,tu,tu,nn,col,sty,2,10,0e0,0e0,0,0e0,0e0,0,0.60,0.95,0.15,0.85, \
          "u0 (rad)","T/T0","Period of nonlinear pendulum")

MainLoop()
```

![](bbox=[0.146, 0.564, 0.856, 0.823])

**FIGURE 12.16** Time dependences of the angular displacement of a nonlinear pendulum for initial displacements equal to 0.1 and, respectively, 3.1, and dependence of the period on the initial displacement $u_0 \in [0.1, 3.1]$ (for Problem 12.7).