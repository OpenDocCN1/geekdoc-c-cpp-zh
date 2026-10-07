# Reliability Block Diagram

The reliability importance of each component is

```
$I_{11}^B = \frac{\partial R_B(t)}{\partial R_{11}(t)} = R_{12}(t)(1 - R_{21}(t)R_{22}(t))(1 - R_{31}(t)R_{32}(t)).
```

```
$I_{12}^B = \frac{\partial R_B(t)}{\partial R_{12}(t)} = R_{11}(t)(1 - R_{21}(t)R_{22}(t))(1 - R_{31}(t)R_{32}(t)).
```

```
$I_{21}^B = \frac{\partial R_B(t)}{\partial R_{22}(t)} = R_{22}(t)(1 - R_{11}(t)R_{12}(t))(1 - R_{31}(t)R_{32}(t)).
```

```
$I_{22}^B = \frac{\partial R_B(t)}{\partial R_{22}(t)} = R_{21}(t)(1 - R_{11}(t)R_{12}(t))(1 - R_{31}(t)R_{32}(t)).
```

```
$I_{31}^B = \frac{\partial R_B(t)}{\partial R_{31}(t)} = R_{32}(t)(1 - R_{11}(t)R_{12}(t))(1 - R_{21}(t)R_{22}(t)).
```

```
$I_{32}^B = \frac{\partial R_B(t)}{\partial R_{32}(t)} = R_{31}(t)(1 - R_{11}(t)R_{12}(t))(1 - R_{21}(t)R_{22}(t)).
```

Considering the reliability of blocks at a specific time $t$ is $R_{11}(t) = 0.95$, $R_{21}(t) = 0.94$, $R_{22}(t) = 0.93$, and $R_{32}(t) = 0.89$, respectively; the reliability importance of each component is $I_{11}^B = 0.0270115$, $I_{12}^B = 0.0272988$, $I_{21}^B = 0.0198025$, $I_{22}^B = 0.0137512$, and $I_{32}^B = 0.0272988$ (see Figure 18.33,a). The maximum reliability importance $MBI = 0.0272988$.

The normalized reliability measures $NI_{11}^B = 0.989474$, $NI_{12}^B = 1$, $NI_{21}^B = 0.717597$, $NI_{31}^B = 0.503729$, and $NI_{32}^B = 0.509389$ (see Figure 18.33,b). These results show that the most important block is the one with smallest reliability that belongs to the series structure that has the highest reliability, since it is a parallel component of two-block series structures.

The Birnbaum importance may also represent the availability importance of components in system [36, 71, 140, 163]. In such cases, we have a partial derivative of the system availability concerning the component $i$’s availability. Transient and steady-state availability may be considered.

```
$I_i^A = \frac{\partial A_s}{\partial A_i} \quad (18.9.5)
```