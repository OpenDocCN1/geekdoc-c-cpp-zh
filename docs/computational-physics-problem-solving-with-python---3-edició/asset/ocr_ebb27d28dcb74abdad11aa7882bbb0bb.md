# Listing 9.3 ProjectileAir.py solves for projectile motion with air resistance as well as analytically for the frictionless case.

```
# ProjectileAir.py: Numerical solution for projectile with drag
from visual import *
from visual.graph import *
v0 = 22.; angle = 34.; g = 9.8; kf = 0.8; N = 5
v0x = v0*cos(angle*pi/180.) v0y = v0*sin(angle*pi/180.)
T = 2.*v0y/g; H = v0y*v0y/2./g; R = 2.*v0x*v0y/g
graph1 = gdisplay(title='Projectile with & without Drag',
xtitle='x', ytitle='y', xmax=R, xmin=-R/20.,ymax=8,ymin=-6.0)
funct = gcurve(color=color.red)
funct1 = gcurve(color=color.yellow)
print(' No Drag T =',T,' H =',H,' R =',R)
def plotNumeric(k):
vx = v0*cos(angle*pi/180.)
vy = v0*sin(angle*pi/180.)
x = 0.0
y = 0.0
dt = vy/g/N/2.
print("\n    With Friction  ")
print("        x            y")
for i in range(N):
rate (30)
vx = vx - k*vx*dt
vy = vy - g*dt - k*vy*dt
x = x + vx*dt
y = y + vy*dt
funct.plot(pos=(x,y))
print(" %13.10f %13.10f"%(x,y))
def plotAnalytic():
v0x = v0*cos(angle*pi/180.)
v0y = v0*sin(angle*pi/180.)
dt = 2.*v0y/g/N
print("\n    No Friction  ")
print("        x            y")
for i in range(N):
rate (30)
t = i*dt
x = v0x*t
y = v0y*t -g*t*t/2.
funct1.plot(pos=(x,y))
print(" %13.10f %13.10f"%(x,y))
plotNumeric(kf)
plotAnalytic()
```

# 9.6.2

# Assessment

+   1. Modify your rk4 program so that it solves the simultaneous ODEs for projectile motion (9.43) with friction (n = 1).
+   2. Check that you obtain graphs similar to those in Figure 9.5.
+   3. The model (9.42) with n = 1 is okay for low velocities. Now modify your program to handle n = 3/2 (medium-velocity friction) and n = 2 (high-velocity friction). Adjust the value of k for the latter two cases such that the initial force of friction k v0^n is the same for all three cases.
+   4. What is your conclusion about balls falling out of the sky?