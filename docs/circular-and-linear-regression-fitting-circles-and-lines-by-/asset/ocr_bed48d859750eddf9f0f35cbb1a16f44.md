|   | 5 | 10 | 15 | 25 | 50 | 100 |
|---|---|---|---|---|---|---|
| 0 | 0.879 | 0.843 | 0.883 | 0.935 | 0.967 | 0.979 |
| 1 | 0.118 | 0.149 | 0.109 | 0.062 | 0.031 | 0.019 |
| \ge 2 | 0.003 | 0.008 | 0.008 | 0.003 | 0.002 | 0.002 |

Table 3.1 Frequency of appearance of 0, 1, 2 or more local minima of F when n = 5, . . . , 100 points are generated randomly with a uniform distribution.

as (3.7) would have many local minima, and the number of local minima would grow with the sample size n. Surprisingly, detailed studies show that this is not the case, in fact quite the opposite is true.

**A numerical search for local minima.** An extensive investigation of local minima of the objective function F was undertaken in [43]. First, the authors plotted F (in a format similar to Fig. 3.6) for a large number of randomly gen- erated samples and visually inspected the plots; in most cases no local minima were visible (Fig. 3.6 is exceptional; it depicts F for a very special, handmade configuration of points).

Next, a sweeping search for local minima was conducted [43] in a ma- chine experiment organized as follows. First, n data points were generated ran- domly from a certain probability distribution. Then the most reliable iterative algorithm (Levenberg-Marquard, which is described in the next chapter) was launched starting at 1000 different, randomly selected initial points (guesses). The idea was that if there were a local minimum, then at least some of the ran- dom initial guesses would fall into its vicinity, attracting the iterations to that minimum. So every point of convergence was recorded as a minimum (local or global) of F. If there were more than one point of convergence, then one of them was the global minimum and the others were local minima. If the al- gorithm converged to the same limit from all the 1000 random initial guesses, the sample was classified as having no local minima.

This search for local minima was then repeated for 10000 different ran- dom samples of n data points generated from the same probability distribution. Then the fraction of simulated samples having 0, 1, 2, etc. local minima was determined, and the results were recorded for the given n and the given proba- bility distribution. This experiment was conducted for different values of n and different probability distributions.

Table 3.1 shows the fraction of simulated samples where F had 0, 1, 2 or more local minima for n = 5, . . . , 100 data points; the probability distribution was uniform in the unit square 0 < x, y < 1 (the size and location of the square do not matter, due to the invariance of the circle fit under translations, rotations, and similarities; see Section 4.11).