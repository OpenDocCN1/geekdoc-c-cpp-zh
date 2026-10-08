# 8.7.3 Computation of Pressure

Problem Compute the pressure at each point and the average pressure over a rectangular area at the bottom of the sea floor for the construction of an oil rig platform. The input to the program is the depth measurements in feet at grid points over a 400-foot by 500-foot rectangular area. The depth measurements are recorded at 50-foot intervals and stored in a file "depth.dat". This example reads a two-dimensional array from a file and processes individual elements.

Method Input the depth measurements (8 rows and 10 columns) and store them in an array depth[8][10]. The formula is derived in Section 6.4.2.

The formula for the computation of pressure is given by:

```
$p = \rho gh$
```

Where

+   * $p$ is the pressure (pounds per square inch),
* $ho$ is the mass density of water (mass per unit volume),
* $g$ is the gravitational acceleration (ft/sec$^2$), and
* $h$ is the depth of water in feet.

```
where $\rho g = 0.4333$
np = 0.4333 * h$ (lbf/inch$^2$)
```

Data Values of depth input from a data file

Pseudocode

```
main:
  input the data
  output the data labeled
  for each grid point
    calculate the pressure
    calculate the average pressure
  output the pressure
  output the average pressure
```

stop