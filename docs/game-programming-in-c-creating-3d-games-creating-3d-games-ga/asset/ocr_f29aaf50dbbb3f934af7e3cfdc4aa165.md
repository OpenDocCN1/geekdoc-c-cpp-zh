![](bbox=[0.15, 0.08, 0.85, 0.33])

Sometimes, the line segment may have multiple points of intersection, as in Figure 10.11(c). Both $P_4$ and $P_5$ intersect the box. In this case, the intersection should return the point closest to the start point, or the one at the lowest $t$ value in the parametric formulation of the line segment.

For the segment tests versus each plane, recall that the equation for line segment versus plane intersection is as follows:

```
t = \frac{-Start \cdot \hat{n} - d}{(End - Start) \cdot \hat{n}}
```

However, because each plane is parallel to a coordinate axis (or, in 3D, a coordinate plane), you can optimize this equation because the normal of each plane will always have zeros for two components and a one for the third component. Thus, two of the three dot product components will always evaluate to zero.

For example, the normal of the left side plane points