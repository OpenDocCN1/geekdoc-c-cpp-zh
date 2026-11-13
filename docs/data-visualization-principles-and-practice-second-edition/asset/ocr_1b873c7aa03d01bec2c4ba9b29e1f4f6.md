![](bbox=[0.056, 0.106, 0.942, 0.246])

Figure 11.11. (a) The tree structure is visualized with (b) a cushion treemap. The actual cushion surface is indicated by the bold black line in (b). The same color is used to indicate the same node in the node-link tree drawing, the treemap, and the cushion profiles.

three levels, whose nodes are colored in hues of blue, green, and red from top to bottom. For every treemap cell, whether it corresponds to a leaf or nonleaf node, we construct a profile whose shape is a convex parabolic function that passes through zero at the cell's borders and reaches maximum at the cell's center. Following the model proposed by van Wijk and van de Wetering [van Wijk and van de Wetering 99], the expression of the parabolic profile for a one-dimensional cell C = [x1, x2] is given by

```
$$h(x) = \frac{4k}{x_2 - x_1} (x - x_1)(x_2 - x).$$ (11.1)
```

Here, the parameter k determines the steepness of the parabolic profile, i.e., the ratio between its height and its width x2 - x1. In Figure 11.11(b), the profiles for each node of the considered tree are drawn with dotted lines.

After we have defined a cushion profile for each treemap cell, we sum up all profiles and define a surface H(x), as indicated by the black bold profile in Figure 11.11(b), which is the sum of the dotted profiles. The one-dimensional equivalent of Figure 11.10 is obtained by rendering this surface illuminated from a direction as indicated in Figure 11.11(b). If we now use increasingly flatter cushions for deeper nodes in the tree, we obtain an image in which the magnitude of the illumination discontinuity, which is proportional to the depth of the "valleys" between neighbor bumps, reflects the depth of the corresponding node in the tree. To achieve this effect, we let the cushion shape parameter k decrease with the depth d in the tree of the considered node, e.g., by setting k = f^d K, where f \in [0, 1] is a flattening factor and K \in [0, 1] the steepness of the top-level, largest cushions.

The shaded cushion construction proceeds similarly for the two-dimensional case. The cushion profiles are now parabolic surfaces instead of curves. The com-