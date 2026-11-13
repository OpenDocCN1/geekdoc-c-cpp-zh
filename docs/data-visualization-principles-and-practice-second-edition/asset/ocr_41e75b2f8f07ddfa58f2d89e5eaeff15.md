For a point \( p \) contained in a line cell \( (p_1, p_2) \), the transformation \( T^{-1} \) is simply the ratio between the lengths of the segment \( pp_1 \) and the cell length, that is

```
\( T_{lin}^{-1}(x, y, z) = \frac{\|p - p_1\|}{\|p_2 - p_1\|}. \) (3.13)
```

# 3.4.3 Triangle

We move now to the next dimension, \( d=2 \). Here, the simplest cell type is the triangle, i.e., \( c = \{v_1, v_2, v_3\} \). Triangles can be used to interpolate along any kind of surfaces embedded in any dimension, e.g., planar or curved surfaces. We can do linear interpolation on triangles. Given the reference triangle cell defined by the points \( v_1 = (0, 0) \), \( v_2 = (1, 0) \), \( v_3 = (0, 1) \), the three linear basis functions are

```
\(\Phi_1^t(r, s) = 1 - r - s,\)
\(\Phi_2^t(r, s) = r,\)
\(\Phi_3^t(r, s) = s.\) (3.14)
```

The transformation \( T^{-1} \) for triangular cells is slightly more complicated than the one for line cells:

```
\( T_{tri}^{-1}(x, y, z) = (r, s) = \left( \frac{\|(p - p_1) \times (p_3 - p_1)\|}{\|(p_2 - p_1) \times (p_3 - p_1)\|}, \frac{\|(p - p_1) \times (p_2 - p_1)\|}{\|(p_3 - p_1) \times (p_2 - p_1)\|} \right) \) (3.15)
```

Figure 3.6 explains this intuitively: Take a triangle \( (p_1, p_2, p_3) \), in world coordinates, and denote its area by \( A_{123} \). Take a point \( p \) in this triangle, and consider the areas \( A_{12} \) and \( A_{13} \) the areas of the triangles \( (p, p_1, p_2) \) and \( (p, p_1, p_3) \), respectively. These quantities are the so-called barycentric coordinates of \( p \) within our triangle. Consider now the area ratios \( r = A_{13}/A_{123} \) and \( s = A_{12}/A_{123} \), which are exactly expressions in Equation 3.15. As \( p \) stays within the initial triangle, both \( r \) and \( s \) are bounded in \( [0, 1] \). Moreover, when \( p = p_1 \), we

![](bbox=[0.2, 0.73, 0.6, 0.85])

Figure 3.6. Coordinate transformation \( T_{tri} \) explained using barycentric coordinates.