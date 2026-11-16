```
[ A_v ]   [  0.1787 ]   [ -1.4630 ]
[ B_v ]   [ -0.3554 ]   [  0.4275 ]
[ C_v ]   [ -0.0227 ] T + [  5.3251 ]
[ D_v ]   [  0.1206 ]   [ -2.5771 ]
[ E_v ]   [ -0.0670 ]   [  0.3703 ]
```

```
[ A_t ]   [ -0.0193 ]   [ -0.2592 ]
[ B_t ]   [ -0.0665 ]   [  0.0008 ]
[ C_t ]   [ -0.0004 ] T + [  0.2125 ]
[ D_t ]   [ -0.0641 ]   [ -0.8989 ]
[ E_t ]   [ -0.0033 ]   [  0.0452 ]
```

```
[ A_r ]   [ -0.0167 ]   [ -0.2608 ]
[ B_r ]   [ -0.0950 ]   [  0.0092 ]
[ C_r ]   [ -0.0079 ] T + [  0.2102 ]
[ D_r ]   [ -0.0441 ]   [ -1.6537 ]
[ E_r ]   [ -0.0109 ]   [  0.0529 ]
```

These values only need to be recomputed if the simulated turbidity level changes, and should be passed into your vertex program as uniform parameters. The result of the Perez function for the sun position and the zenith xyY color should also be uniform parameters, as well as the position of the sun (or moon).

With these values and the position of each vertex in your skybox, you have everything you need for your physically-based skybox vertex program to compute xyY values for each sky vertex. The last step is to map this result to RGB values. To do this, first convert the xyY value to XYZ:

```
X = x \frac{Y}{y}
Z = (1 - x - y) \frac{Y}{y}.
```

If the zenith color you're using is already tone mapped, then further tone mapping is optional. The same tone mapping technique described in "Physically-Based Outdoor Scene Lighting" may be applied at this point, however, and will result in effects such as a