![](bbox=[0.18, 0.08, 0.92, 0.31])

FIGURE 4.2.1 The iWave approximation of a planar body of water. Three-dimensional (left) and two-dimensional (right) depictions are shown.

To animate the system, two grids are used, representing the pre and post state of a time step. One grid stores the current height values of the system. It is then used to calculate the values of the next time step, stored in the other grid. Using two grids ensures the calculations performed on the (i - 1, j) point for example, do not bleed over onto point (i, j).

To make waves move through the system, we look at each point (i, j) individually. The resulting height at that point is calculated by summing the heights of the point around it, dividing the result by two, and subtracting the height of the current point:

```
res_h[i,j] = (src_h[i-1,j] +
                      src_h[i+1,j] +
                      src_h[i,j-1] +
                      src_h[i,j+1] ) / 2 - src_h[i,j];
```

The result is a system where waves move through the grid. The waves maintain the same amplitude, so energy has to be removed from the system. The solution is to simply remove a portion of the energy from the system every update by subtracting a portion of the height:

```
res_h[i,j] := res_h[i,j] * damp_factor;
```

To create a ripple on the surface, simply set the height point on the surface to a value other than 0. The effect is that the change produced moves throughout the system, affecting points around the selected point. A wave, in turn, ripples out from the selected point.

Specifics as to how and why these formulas are used and why they work are found in [Willems00] and are more thoroughly discussed in [GPG04] (including how to animate over a variable time step). The effect conserves water mass; as a surface rises