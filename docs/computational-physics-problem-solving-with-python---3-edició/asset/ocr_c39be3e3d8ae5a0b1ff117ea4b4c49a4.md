![](bbox=[0.18, 0.12, 0.58, 0.28])

Figure 17.10 The analytic and quantum Monte Carlo solution for the quantum bouncer. The continuous line is the Airy function squared and the dashed line |ψ₀(z)|² after a million trajectories.

|ψ(0)|² ≈ 0 (the boundary condition). To account for the fact that the potential is infinite for negative x values, we selected trajectories that have positive x values over all their links. This incorporates the fact that the particle can never penetrate the floor. Our program is given in Listing 17.4, and it yields the results in Figure 17.10 after using 10⁶ trajectories and a time step ε = dτ = 0.05. Both results were normalized via a trapezoid integration. As can be seen, the agreement between the analytic result and the path integration is satisfactory.

# Listing 17.4 QMCbouncer.py uses Feynman path integration to compute the path of a quantum particle in a gravitational field.

```
# QMCbouncer.py:        g.s. wavefunction via path integration
from visual import *
import random
from visual.graph import *
# Parameters
N = 100;  dt = 0.05;          g = 2.0;        h = 0.00;        maxel = 0
path = zeros([101], float);   arr = path; prob = zeros([201],float)
trajec = display(width = 300, height=500,title = 'Spacetime Trajectory')
trplot = curve(y = range(0, 100), color=color.magenta, display = trajec)
def trjaxs():                # plot axis for trajectories
    trax=curve(pos=[(-97,-100),(100,-100)],color=color.cyan,display=trajec)
    curve(pos = [(-65, -100),(-65, 100)], color=color.cyan,display=trajec)
    label(pos = (-65,110), text = 't', box = 0, display = trajec)
    label(pos = (-85, -110), text = '0', box = 0, display = trajec)
    label(pos = (60, -110), text = 'x', box = 0, display = trajec)
    wvgraph = display(x=350, y=80, width=500, height=300, title = 'GS Prob')
    wvplot  = curve(x = range(0, 50), display = wvgraph)  # wave function plot
    wvfax   = curve(color = color.cyan)
def wvfaxs():                # plot axis for wavefunction
    wvfax = curve(pos
    =[(-200,-155),(800,-155)],display=wvgraph,color=color.cyan)
    curve(pos = [(-200,-150),(-200,400)],display=wvgraph,color=color.cyan)
    label(pos = (-70, 420),text = 'Probability', box = 0, display=wvgraph)
    label(pos = (600, -220),text = 'x', box = 0, display = wvgraph)
    label(pos = (-200, -220),text = '0', box = 0, display = wvgraph)
```