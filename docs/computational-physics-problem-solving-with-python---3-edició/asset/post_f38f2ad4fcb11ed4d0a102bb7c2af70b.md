
## Listing 8.1 rk4.py solves an ODE with the RHS given by the method f() using a fourth-order Runge–Kutta algorithm. Note that to avoid introducing bugs, the method f(), which you will need to change for each problem, is kept separate from the algorithm.

```
# rk4.py 4th order Runge Kutta

from visual.graph import *

#   Initialization
a = 0.
b = 10.
n = 100
ydumb = zeros((2), float);   y = zeros((2), float)
fReturn = zeros((2), float);  k1 = zeros((2), float)
k2 = zeros((2), float);      k3 = zeros((2), float)
k4 = zeros((2), float)
y[0] = 3.;   y[1] = -5.
t = a;      h = (b-a)/n;

def f(t, y):                                   # Force function
    fReturn[0] = y[1]
    fReturn[1] = -100.*y[0]-2.*y[1] + 10.*sin(3.*t)
    return fReturn

graph1 = gdisplay(x=0,y=0, width = 400, height = 400, title = 'RK4',
                  xtitle = 't', ytitle = 
                  'Y[0]',xmin=0,xmax=10,ymin=-2,ymax=3)
funct1 = gcurve(color = color.yellow)
graph2 = gdisplay(x=400,y=0, width = 400, height = 400, title = 'RK4',
                  xtitle = 't', ytitle = 
                  'Y[1]',xmin=0,xmax=10,ymin=-25,ymax=18)
funct2 = gcurve(color = color.red)

def rk4(t,h,n):
    k1 = [0]*(n)
    k2 = [0]*(n)
    k3 = [0]*(n)
    k4 = [0]*(n)
    fR = [0]*(n)
    ydumb = [0]*(n)
    fR = f(t, y)                               # Returns RHS's
    for i in range(0, n):
        k1[i] = h*fR[i]
    for i in range(0, n):
        ydumb[i] = y[i] + k1[i]/2.
    k2 = h*f(t+h/2., ydumb)
    for i in range(0, n):
        ydumb[i] = y[i] + k2[i]/2.
    k3 = h*f(t+h/2., ydumb)
    for i in range(0, n):
        ydumb[i] = y[i] + k3[i]
    k4 = h*f(t+h, ydumb)
    for i in range(0, n, 2):
        y[i] = y[i] + (k1[i] + 2.*(k2[i] + k3[i]) + k4[i])/6.
    return y

while (t < b):                                 # Time loop
    if ((t + h) > b):
        h = b - t                              # Last step
    y = rk4(t,h,2)
    t = t + h
    rate(30)
    funct1.plot(pos = (t, y[0]) )
    funct2.plot(pos = (t, y[1]) )
```

A variation of rk4, known as the Runge–Kutta–Fehlberg method (Mathews, 2002), or rk45, varies the step size while doing the integration with the hope of obtaining better precision and maybe better speed. Our implementation, rk45.py, is given in Listing 8.2. It automatically doubles the step size and tests to see how an estimate of the error changes. If the error is still within acceptable bounds, the algorithm will continue to use the larger step size and thus speed up the computation; if the error is too large, the algorithm will decrease the step size until an acceptable error is found. As a consequence of the extra information obtained in the testing, the algorithm does obtain O(h^5) precision, but sometimes at the expense of extra computing time. Whether that extra time is recovered by being able to use a larger step size depends upon the application.

**Listing 8.2** **rk45.py** solves an ODE with the RHS given by the method *f()* using a fourth-order Runge–Kutta algorithm with adaptive step size.

```
# rk45.py                 Adaptive step size Runge Kutta

from visual.graph import *

a = 0.; b = 10.                         # Error tolerance, endpoints
Tol = 1.0E-8
vdum = zeros((2), float)                 # Initialize
y = zeros((2), float)
fReturn = zeros((2), float)
err = zeros((2), float)
k1 = zeros((2), float)
k2 = zeros((2), float)
k3 = zeros((2), float)
k4 = zeros((2), float)
k5 = zeros((2), float)
k6 = zeros((2), float)
n = 20
y[0] = 1.;  y[1] = 0.

h = (b - a)/n;  t = a;  j = 0
hmin = h/64;  hmax = h*64                  # Min and max step sizes
flops = 0;  Eexact = 0.;  error = 0.
sum = 0.

def f(t, y, fReturn ):                    # Force function
    fReturn[0] = y[1]
    fReturn[1] = - 6.*pow(y[0], 5.)

graph1 = gdisplay(width = 600, height = 600, title = 'RK 45',
                  xtitle = 't', ytitle = 'Y[0]')
funct1 = gcurve(color = color.blue)
graph2 = gdisplay(width = 500, height = 500, title = 'RK45',
                  xtitle = 't', ytitle = 'Y[1]')
funct2 = gcurve(color = color.red)
funct1.plot(pos = (t, y[0]))
funct2.plot(pos = (t, y[1]))

while (t < b):                         # Loop over time
    funct1.plot(pos = (t, y[0]))
    funct2.plot(pos = (t, y[1]))
    if ((t + h) > b):
        h = b - t                         # Last step
    f(t, y, fReturn)                       # Evaluate f, return in fReturn
    k1[0] = h*fReturn[0];      k1[1] = h*fReturn[1]
    for i in range(0, 2):
```

```
ydumb[i] = y[i] + k1[i]/4
f(t + h/4, ydumb, fReturn)
k2[0] = h*fReturn[0];    k2[1] = h*fReturn[1]
for i in range(0, 2):
    ydumb[i] = y[i] + 3*k1[i]/32 + 9*k2[i]/32
f(t + 3*h/8, ydumb, fReturn)
k3[0] = h*fReturn[0];    k3[1] = h*fReturn[1]
for i in range(0, 2):
    ydumb[i] = y[i] + 1932*k1[i]/2197 - 7200*k2[i]/2197. + 7296*k3[i]/2197
f(t + 12*h/13, ydumb, fReturn)
k4[0] = h*fReturn[0]; k4[1] = h*fReturn[1]
for i in range(0, 2):
    ydumb[i] = y[i] + 439*k1[i]/216 - 8*k2[i] + 3680*k3[i]/513 - 845*k4[i]/4104
f(t + h, ydumb, fReturn)
k5[0] = h*fReturn[0]; k5[1] = h*fReturn[1]
for i in range(0, 2):
    ydumb[i] = y[i] - 8*k1[i]/27 + 2*k2[i] - 3544*k3[i]/2565 + 1859*k4[i]/4104 - 11*k5[i]/40
f(t + h/2, ydumb, fReturn)
k6[0] = h*fReturn[0]; k6[1] = h*fReturn[1];
for i in range(0, 2):
    err[i] = abs( k1[i]/360 - 128*k3[i]/4275 - 2197*k4[i]/75240 + k5[i]/50. + 2*k6[i]/55)
if ( err[0] < Tol or err[1] < Tol or h <= 2*hmin ):  # Accept step
    for i in range(0, 2):
        y[i] = y[i] + 25*k1[i]/216. + 1408*k3[i]/2565. + 2197*k4[i]/4104. - k5[i]/5.
    t = t + h
    j = j + 1
if ( err[0] == 0 or err[1] == 0 ):
    s = 0                                   # Trap division by 0
else:
    s = 0.84*pow(Tol*h/err[0], 0.25)        # Reduce step
if ( s < 0.75 and h > 2*hmin ):
    h /= 2.                                 # Increase step
else:
    if ( s > 1.5 and 2*h < hmax ):
        h *= 2.
flops = flops + 1
E = pow(y[0], 6.) + 0.5*y[1]*y[1]
Eexact = 1.
error = abs( (E - Eexact)/Eexact )
sum += error
print(" <error>= ", sum/flops , ", flops = ", flops)
```

## 8.7

## Adams–Bashforth–Moulton Predictor–Corrector Rule

Another approach for obtaining high precision in an ODE algorithm uses the solution from previous steps y_{n-2} and y_{n-1}, in addition to y_n, to predict y_{n+1}. (The Euler and rk methods use just one previous step.) Many of these types of methods tend to be like a Newton’s search method; we start with a guess or prediction for the next step and then use an algorithm such as rk4 to check on the prediction and thereby obtain a correction. As with rk45, one can use the correction as a measure of the error and then adjust the step size to obtain improved precision (Press et al., 1994). For those readers who may want to explore such methods, ABM.py in List-

```
p = y[k] + h2*(-9.*F0 + 37.*F1 - 59.*F2 + 55.*F3)
    t[k + 1] = a + h*(k+1)                     # Next abscissa
    F4 = f(t[k+1], p)
    y[k+1] = y[k] + h2*(F1-5.*F2 + 19.*F3 + 9.*F4)   # Corrector
    F0 = F1
    F1 = F2
    F2 = F3
    F3 = f(t[k + 1], y[k + 1])
    return t,y

print(" k          t          Y numerical      Y exact")
t, y = ABM(A,B,n)
for k in range(0, n+1):
    print(" %3d %5.3f %12.11f %12.11f "
          % (k,t[k],y[k],(3.*exp(-t[k]/2.)-2.+t[k])))
    numsol.plot(pos = (t[k], y[k]))
    exsol.plot(pos = (t[k], 3.*exp(-t[k]/2.) -2. + t[k]))
```

### 8.7.1

## Assessment: rk2 vs. rk4 vs. rk45

While you are free to do as you please, unless you are very careful, we recommend that you not write your own rk4 or rk45 methods. You will be using this code for some high-precision work, and unless you get every fraction and method call just right, your code may appear to work well but still not give all the precision that you should be obtaining, and therefore we give you rk4, and rk45 codes to use. However, we do recommend that you write your own rk2, as doing so will make it clearer as to how the Runge–Kutta methods work, but without all the pain and danger.

- 1. Write your own rk2 method. Design your method for a general ODE; this means making the derivative function f(t,x) a separate method.
- 2. Use your rk2 solver in a program that solves the equation of motion (8.7) or (8.25). Plot both the position x(t) and velocity dx/dt as functions of time.
- 3. Once your ODE solver is running, do a number of things to check that it is working well and that you know what h values to use.
  - a) Adjust the parameters in your potential so that it corresponds to a pure harmonic oscillator (set p = 2 or a = 0). For an oscillator initially at rest, we have an analytic result with which to compare:
    x(t) = A sin(ω₀ t),    v = ω₀ A cos(ω₀ t),    ω₀ = √(k/m).    (8.40)
  - b) Pick values of k and m such that the period T = 2π/ω is a nice number with which to work (something like T = 1).
  - c) Start with a step size h ≈ T/5 and make h smaller until the solution looks smooth, has a period that remains constant for a large number of cycles, and agrees with the analytic result. As a general rule of thumb, we suggest that you start with h ≈ T/100, where T is a characteristic time for the problem at hand. You should start with a large h so that you can see a bad solution turn good.
