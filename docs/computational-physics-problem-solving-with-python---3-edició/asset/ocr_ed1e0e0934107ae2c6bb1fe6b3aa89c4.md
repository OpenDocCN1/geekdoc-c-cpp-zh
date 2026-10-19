Listing 11.7 Tune.py is meant to be numerically intensive enough to show the results of various types of optimizations, but you may need to increase sizes to make

it more intensive. The program solves the eigenvalue problem iteratively for a nearly diagonal Hamiltonian matrix using a variation of the power method.

```
# Tune.py Basic tuning program showing memory allocation
import datetime; from numpy import zeros; from math import (sqrt, pow)
Ldim = 251;     iter = 0;       step = 0.
diag = zeros((Ldim, Ldim), float);   coef = zeros( (Ldim), float)
sigma = zeros((Ldim), float);        ham = zeros( (Ldim, Ldim), float)
t0 = datetime.datetime.now()                # Initialize
time
for i in range(1, Ldim):                    # Set up
    Hamiltonian
    for j in range(1, Ldim):
        if (abs(j - i) )>10: ham[j, i] = 0.
        else : ham[j, i] = pow(0.3, abs(j - i) )
    ham[i,i] = i ;
coef[1] = 1.;        err = 1.;      iter = 0 ;
print("iter   ener      err ")
while (iter < 15 and err > 1.e-6):      # Compute current E &
    normalize
    iter = iter + 1; ener = 0.; ovlp = 0.;
    for i in range(1, Ldim):
        ovlp = ovlp + coef[i]*coef[i]
        sigma[i] = 0.
        for j in range(1, Ldim): sigma[i] = sigma[i] +
            coef[j]*ham[j][i]
        ener = ener + coef[i]*sigma[i]
    ener = ener/ovlp
    for i in range(1, Ldim):
        coef[i] = coef[i]/sqrt(ovlp)
        sigma[i] = sigma[i]/sqrt(ovlp)
    err = 0.;
    for i in range(2, Ldim):
        Update
        step = (sigma[i] - ener*coef[i])/(ener - ham[i, i])
        coef[i] = coef[i] + step
        err = err + step*step
    err = sqrt(err)
    print "%2d  %9.7f  %9.7f"%(iter, ener, err)
delta_t = datetime.datetime.now() - t0      # Elapsed
time
print "time = ", delta_t
```

13. Make a graph of run time vs. matrix size. It should be similar to Figure 11.1, although if there is more than one user on your computer while you run, you may get erratic results. Note that as our matrix becomes larger than ~ 1000 × 1000 in size, the curve sharply increases in slope with execution time, in our case increasing like the third power of the dimension. Because the number of elements to compute increases as the second power of the dimension, something else is happening here. It is a good guess that the additional slowdown is as a result of page faults in accessing memory. In particular, accessing 2D arrays, with their elements scattered all through memory, can be very slow.