![](bbox=[0.12, 0.12, 0.86, 0.28])

(a) (b)

Figure 1.6 (a,b) Columns show two separate outputs, each of two figures, produced by MatPlot2figs.py. (We used the slider button to add some space between the plots.)

placed two curves in one plot, and then output two different figures, each containing two plots. The key here is the repetition of the subplot command:

| figure(1) | # The 1st figure |
| subplot(2,1,1) | # 2 rows, 1 column, 1st subplot |
| subplot(2,1,2) | # 2 rows, 1 column, 2nd subplot |

The listing is self-explanatory, with sections that set the plotting limits, that creates each figure, and then creates the grid.

# Listing 1.7 PondMatPlot.py produces the scatter plot and the curve shown in Figure 5.5 in Chapter 5.

```
# PondMatPlot.py: Monte-Carlo integration via vonNeumann rejection
import numpy as np
import matplotlib.pyplot as plt

N = 100
x1 = np.arange(0, 2*np.pi+2*np.pi/N,2*np.pi/N)
fig,ax = plt.subplots()
y1 = x1 * np.sin(x1)**2                # Integrand
ax.plot(x1, y1, 'c-', linewidth=4)
ax.set_xlim((0, 2*np.pi))
ax.set_ylim((0, 5))
ax.set_yticks([0, np.pi, 2*np.pi])
ax.set_xticklabels(['0', '$\uppi$', '2$\uppi$'])
ax.set_ylabel('$f(x) = x\sin^2 x$', fontsize=20)
ax.set_xlabel('x', fontsize=20)
fig.patch.set_visible(False)
xi=[]; yi=[]; xo=[]; yo=[]

def fx(x):                             # Integrand
    return x*np.sin(x)**2

j = 0                                  # Inside curve counter
Npts = 3000
analyt = np.pi**2
xx = 2.* np.pi * np.random.rand(Npts)  # 0 <= x <= 2pi
 yy = 5*np.random.rand(Npts)           # 0 <= y <= 5
for i in range(1,Npts):
```