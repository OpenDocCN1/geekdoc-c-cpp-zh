```
nn = [0, n, 2*n, 3*n]
col = ["", "blue", "green", "red"]
sty = [0, 1, 1, 1]
MultiPlot(x,y,y,nn,col,sty,3,10,
    0e0,0e0,0,0e0,0e0,0,0.10,0.45,0.15,0.85,
    "lambda (micron)","u","Spectral energy density")

MultiPlot(x,z,z,nn,col,sty,3,10,
    0e0,0e0,0,0e0,0e0,0,0.60,0.95,0.15,0.85,
    "lambda (micron)","du","Derivative of energy density")

#--------------------------------------------------------------------
T = 5778e0                     # temperature of sun's photosphere
lam0 = h*kB / (kB*T)           # reference wavelength
K = 8e0 * pi * kB * T / pow(lam0,4)   # factor of u(lam)

fmin = 1e10; fmax = -1e10       # positions of maximum and minimum of du
for i in range(1,n+1):
    lam = (i-1)*h; f = du(lam)
    if (f > fmax): fmax = f; lam_1 = lam          # maximum
    if (f < fmin): fmin = f; lam_2 = lam          # minimum

lam_max = 0.5e0 * (lam_1 + lam_2)               # find zero of du in [lam_1,lam_2]
(lam_max,iierr) = NewtonNumDrv(du,lam_1,lam_2,lam_max)   # initial approximation
print("Wien's law:")
print("T = {0:4.0f} K".format(T))
print("lambda_max = {0:e} m".format(lam_max))
print("lambda_max * T = {0:e} m K".format(lam_max * T))   # 2.897768e-3 m K

MainLoop()
```

![](bbox=[0.13, 0.61, 0.85, 0.86])

FIGURE 6.10 Planck's law of black-body radiation: spectral energy density u(λ, T) (left panel) and derivative ∂u(λ, T)/∂λ, for T = 4000, 5000, and 6000 K, corresponding to major peaks of increasing magnitude.