![](bbox=[0.12, 0.1, 0.33, 0.27])

![](bbox=[0.37, 0.1, 0.68, 0.27])

Figure 15.5 (a) Position vs. time for two initial conditions of a chaotic pendulum that end up with the same limit cycle. (b) A phase space plot of position versus velocity for the limit cycle shown in (a) (courtesy of W. Hager).

so rich in complexity. The solutions are easier to understand in phase space, particularly if you learn to recognize some characteristic structures there. Actually, there are a number of “tools” that can be used to decide if a system is chaotic in contrast to just complex. Geometric structures in phase space is one of them, and determination of the Lyapunov coefficient (discussed in Section 14.8) is another. Both signal the simplicity lying within the complexity.

What may be surprising is that even though the ellipse-like figures in phase space were observed originally for free systems with no friction and no driving torque, similar structures continue to exist for driven systems with friction. The actual trajectories may not remain on a single structure for all times, but they are attracted to them and return to them often. In contrast to periodic motion which produces closed figures in phase-space, random motion appears as a diffuse cloud filling the entire energetically accessible region. Complex or chaotic motion falls someplace in between (Figure 15.6b). If viewed for long times and for many initial conditions, chaotic trajectories in phase space, while resembling the familiar geometric figures, may contain dark or diffuse bands rather than single lines. The continuity of trajectories within bands means that a continuum of solutions are possible and that the system flows continuously among the different trajectories forming the band. The transitions among different phase-space orbits appear chaotic in normal space. The bands are what makes the solutions hypersensitive to the initial conditions as the slightest change in them causes the system to flow to nearby phase-space trajectories.

Pick out the following phase-space structures in your simulations:

Limit cycles When a chaotic pendulum is driven by a not-too-large driving torque, it is possible to pick the magnitude for this torque such that after the initial transients die off, the average energy put into the system during one period exactly balances the average energy dissipated by friction during that period (Figure 15.5):

```
<f cos ωt> = <α dθ/dt> = <α dθ(0)/dt cos ωt> ⇒ f = α dθ(0)/dt . (15.14)
```