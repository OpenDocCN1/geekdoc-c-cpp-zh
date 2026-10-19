We eliminate the ψ⁽⁴⁾ terms by substituting the derived expression for the ψ⁽²⁾:

ψ(x + h) + ψ(x − h) − 2ψ(x) / h² + k²(x)ψ(x) + h²/12 d²/dx² [k²(x)ψ(x)] ≃ 0 . (9.18)

Now we use a central-difference approximation for the second derivative of k²(x)ψ(x):

h² d²[k²(x)ψ(x)]/dx² ≃ [(k²ψ)_{x+h} − (k²ψ)_x] + [(k²ψ)_{x−h} − (k²ψ)_x] . (9.19)

After this substitution, we obtain the Numerov algorithm:

ψ(x + h) ≃ { 2[1 − 5/12 h²k²(x)] ψ(x) − [1 + h²/12 k²(x − h)] ψ(x − h) } / { 1 + h²k²(x + h)/12 } . (9.20)

We see that the Numerov algorithm uses the values of ψ at the two previous steps x and x − h to move ψ forward to x + h. To step backward in x, we need only to reverse the sign of h. Our implementation of this algorithm, Numerov.py, is given in Listing 9.1.

# Listing 9.1 QuantumNumerov.py solves the 1D time-independent Schrödinger equation for bound-state energies using a Numerov method (rk4 also works, as we show in Listing 9.2).

```
# QuantumNumerov: Quantum BS via Numerov ODE solver + search
from visual import *
from visual.graph import *
psigr = display(x=0, y=0, width=600,height=300,title='R & L Wave Funcs')
psi = curve(x=list(range(0,1000)), display=psigr, color=color.yellow)
psi2gr = display(x=0,y=300,width=600,height=200,title='Wave func'2')
psio = curve(x=list(range(0,1000)),color=color.magenta, display=psi2gr)
energr = display(x=0, y=500, width=600,height=200,title='Potential & E')
poten = curve(x=list(range(0,1000)), color=color.cyan, display=energr)
autoen = curve(x=list(range(0,1000)), display=energr)

dl = 1e-6 # very small interval to stop bisection
ul = zeros([1501], float)
ur = zeros([1501], float)
k2l = zeros([1501], float) # k**2 left wavefunc
k2r = zeros([1501], float)
n = 1501
m = 5 # plot every 5 points
imax = 100
xl0 = -1000; xr0 = 1000 # leftmost, rightmost x
h = 1.0*(xr0-xl0)/(n-1)
amin = -0.001; amax = -0.00085 # root limits
e = amin # Initial E guess
de = 0.01
ul[0] = 0.0; ul[1] = 0.00001; ur[0] = 0.0; ur[1] = 0.00001
im = 500
nl = im+2; nr = n-im+1 # left, right wv
istep = 0
```