If our actual quad cells are rectangular instead of arbitrary quads, like in a uniform or rectilinear grid, we can do better. In that case, the transformation \( T_{\text{rect}}^{-1} \) consists of two line transformations \( T_{\text{lin}}^{-1} \). Given a quad cell with vertices \( p_1, p_2, p_3, p_4 \), we have

```
\( T_{\text{rect}}^{-1}(x, y, z) = (r, s) = \left( \frac{(p - p_1) \cdot (p_2 - p_1)}{\|p_2 - p_1\|^2}, \frac{(p - p_1) \cdot (p_4 - p_1)}{\|p_4 - p_1\|^2} \right). \) (3.17)
```

# 3.4.5 Tetrahedron

We now move to the next dimension, \( d=3 \). Here, the simplest cell type is the tetrahedron, defined by its four vertices \( c = (v_1, v_2, v_3, v_4) \). On the reference tetrahedron defined by the points \( v_1 = (0, 0, 0) \), \( v_2 = (1, 0, 0) \), \( v_3 = (0, 1, 0) \), \( v_4 = (0, 0, 1) \), the four linear basis functions are

```
\(\Phi_1(r, s, t) = 1 - r - s - t,\)
\(\Phi_2(r, s, t) = r,\)
\(\Phi_3(r, s, t) = s,\)
\(\Phi_4(r, s, t) = t.\) (3.18)
```

Given a tetrahedral cell with vertices \( p_1, p_2, p_3, p_4 \), we can deduce the transformation \( T_{\text{tet}}^{-1} \) using the barycentric coordinate idea outlined for \( T_{\text{tri}}^{-1} \) (see Section 3.4.3). In detail, if \( T_{\text{tet}}^{-1}(x, y, z) = (r, s, t) \), then the reference coordinates \( r \), \( s \), and \( t \) of the point \( p = (x, y, z) \) can be computed as the ratio of the volumes of the tetrahedra \( (p, p_1, p_3, p_4) \), \( (p, p_1, p_2, p_4) \), and \( (p, p_1, p_2, p_3) \) to the volume of \( (p_1, p_2, p_3, p_4) \). This gives the following formulas for the reference coordinates:

```
\( r = \frac{|(p - p_4) \cdot ((p_1 - p_4) \times (p_3 - p_4))|}{|(p_1 - p_4) \cdot ((p_2 - p_4) \times (p_3 - p_4))|},\)
\( s = \frac{|(p - p_4) \cdot ((p_1 - p_4) \times (p_2 - p_4))|}{|(p_1 - p_4) \cdot ((p_2 - p_4) \times (p_3 - p_4))|},\)
\( t = \frac{|(p - p_3) \cdot ((p_1 - p_3) \times (p_2 - p_3))|}{|(p_4 - p_3) \cdot ((p_2 - p_3) \times (p_1 - p_3))|}.\) (3.19)
```

Some applications also use pyramid cells and prism cells to discretize volumetric domains (see Figure 3.5). To limit the number of cell types we need to support in a concrete software implementation, pyramid and prism cells can be split into tetrahedral cells, similar to the way we split quad cells into two triangle cells.