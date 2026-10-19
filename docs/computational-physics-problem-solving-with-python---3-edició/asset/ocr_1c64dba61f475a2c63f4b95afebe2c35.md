```
```python
y[i] = y[i] + h*(vy[i] + hover2*fy[i][t1]);
    if x[i] <= 0.:
        x[i] = x[i] + L              # Periodic boundary conditions
    if x[i] >= L:
        x[i] = x[i] - L
    if y[i] <= 0.:
        y[i] = y[i] + L
    if y[i] >= L:
        y[i] = y[i] - L
    xc = 2*x[i] - 4
    yc = 2*y[i] - 4
    atoms[i].pos=(xc,yc)
PE = 0.
t2=1
PE = Forces(t2, w, PE, 1)
KE = 0.
w = 0.
for i in range(0 , Natom):
    vx[i] = vx[i] + hover2*(fx[i][t1] + fx[i][t2])
    vy[i] = vy[i] + hover2*(fy[i][t1] + fy[i][t2])
    KE = KE + (vx[i]*vx[i] + vy[i]*vy[i])/2
w = Forces(t2, w, PE, 2)
P=dens*(KE+w)
T=KE/(Natom)
# increment averages
avT = avT + T
avP = avP + P
avKE = avKE + KE
avPE = avPE + PE
time += 1
t=time
if (t == 0):
    t=1
Pavg = avP / t
eKavg = avKE / t
ePavg = avPE / t
Tavg = avT / t
pre = (int)(Pavg*1000)
Pavg = pre/1000.0
kener = (int)(eKavg*1000)
eKavg = kener/1000.0
Kavegraph.plot(pos=(t,eKavg))
pener = (int)(ePavg*1000)
ePavg = pener/1000.0
tempe = (int)(Tavg*1000000)
Tavg = tempe/1000000.0
Tcurve.plot(pos=(t,ePavg),display=sceneT)

timevolution()
```
```

The program MD.py in Listings 18.1 implements an MD simulation in 1D using the velocity-Verlet algorithm. Use it as a model and do the following:

+   1. Establish that you can run and visualize the 1D simulation.
+   2. Place the particles initially at the sites of a simple cubic lattice. The equilibrium configuration for a Lennard–Jones system at low temperature is a face-centered-cubic, and if your simulation is running properly, then the particles should migrate from SC to FCC. An FCC lattice has four quarters of a particle per unit cell, so an $L^3$ box with a lattice constant $L/N$ contains (parts of) $4N^3 = 32, 108, 256, \ldots$ particles.