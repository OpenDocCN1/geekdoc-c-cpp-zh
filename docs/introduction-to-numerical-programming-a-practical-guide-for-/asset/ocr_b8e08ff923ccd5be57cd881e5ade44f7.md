```
def ProbDens(Psi, Psi2, nx, hx):
#-------------------------------------------------------------------------------
# Calculates the probability density Psi2[] of the wave function Psi[]
#-------------------------------------------------------------------------------
    for i in range(1,nx+1):
        Psi2[i] = abs(Psi[i])*abs(Psi[i])      # unnormalized probability density
        if (Psi2[i] <= 1e-10): Psi2[i] = 0e0

    PsiNorm = 0.5e0*(Psi2[1] + Psi2[nx])          # integral by trapezoidal rule
    for i in range(2,nx): PsiNorm += Psi2[i]
    PsiNorm *= hx

    for i in range(1,nx+1): Psi2[i] /= PsiNorm      # normalized prob. density
    return PsiNorm

# main

a    = 5e0                                   # width of potential barrier
V0   = 25e0                                 # height of potential barrier
x0   = -20e0                                # initial position of wave packet
sig  = 1e0                                  # half-width of packet
k0   = 10e0                                 # average wave number of packet
xmax = 100e0                                # maximum x
hx   = 5e-2                                 # spatial step size
tmax = 5e0                                  # maximum propagation time
h t   = 5e-3                                 # time step
nout = 40                                   # output every nout steps

nx = 2*(int)(xmax/hx + 0.5) + 1             # odd number of spatial nodes
nt = (int)(tmax/ht + 0.5)                   # number of time steps
nx2 = int(nx/2); nx4 = int(nx/4) + 1

Psi  = [complex(0,0)]*(nx+1)                # wave function
Psi2 = [0]*(nx+1)                           # probability density
V    = [0]*(nx+1)                           # potential
x    = [0]*(nx+1)                           # spatial mesh

for i in range(1,nx+1):                     # tabulate spatial mesh and potential
    x[i] = (i-nx2-1)*hx
    V[i] = Pot(x[i],a,V0)

Init(Psi,x,nx,x0,sig,k0)                    # initial wave packet

GraphInit(1000,700)

for it in range(1,nt+1):                    # time loop
    t = it*ht
    PropagQTD(Psi,V,nx,hx,ht)               # propagate solution by tridiagonal solver

    PsiNorm = ProbDens(Psi,Psi2,nx,hx)      # probability density

    if (it % nout == 0 or it == nt):        # output every nout steps
        fname = "scatter_{0:4.2f}.txt".format(t)
        out = open(fname,"w")
        out.write("t = {0:4.2f}\n".format(t))
        out.write("     x          V          PsiR        PsiI        Psi2\n")
        for i in range(1,nx+1):
            out.write("{0:10.5f}{1:10.5f}{2:10.5f}{3:10.5f}\n".\
                    format(x[i],V[i],Psi[i].real,Psi[i].imag,Psi2[i]))
```