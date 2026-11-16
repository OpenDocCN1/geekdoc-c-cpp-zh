product with itself—you can simplify p as follows:

```
\bar{p} = \left( \overrightarrow{AC} \cdot \frac{\overrightarrow{AB}}{\|\overrightarrow{AB}\|} \right) \frac{\overrightarrow{AB}}{\|\overrightarrow{AB}\|} = \frac{\overrightarrow{AC} \cdot \overrightarrow{AB}}{\|\overrightarrow{AB}\|} \frac{\overrightarrow{AB}}{\|\overrightarrow{AB}\|} = \frac{\overrightarrow{AC} \cdot \overrightarrow{AB}}{\|\overrightarrow{AB}\|^2} \overrightarrow{AB}
= \frac{\overrightarrow{AC} \cdot \overrightarrow{AB}}{\overrightarrow{AB} \cdot \overrightarrow{AB}} \overrightarrow{AB}
```

```
\bar{p} = \left( \overrightarrow{AC} \cdot \frac{\overrightarrow{AB}}{\|\overrightarrow{AB}\|} \right) \frac{\overrightarrow{AB}}{\|\overrightarrow{AB}\|} = \frac{\overrightarrow{AC} \cdot \overrightarrow{AB}}{\|\overrightarrow{AB}\|} \frac{\overrightarrow{AB}}{\|\overrightarrow{AB}\|}
= \frac{\overrightarrow{AC} \cdot \overrightarrow{AB}}{\|\overrightarrow{AB}\|^2} \overrightarrow{AB}
= \frac{\overrightarrow{AC} \cdot \overrightarrow{AB}}{\overrightarrow{AB} \cdot \overrightarrow{AB}} \overrightarrow{AB}
```

Finally, you construct the vector from p to AC, and the length of this vector is the minimum distance from AB to C:

```
d = \|\overrightarrow{AC} - \bar{p}\|
d = \|\overrightarrow{AC} - \vec{p}\|
```

Remember that because the distance must be positive in this case, you can square both sides of the equation to instead get the minimal distance squared from AB to C:

```
d^2 = \|\overrightarrow{AC} - \bar{p}\|^2
d^2 = \|\overrightarrow{AC} - \vec{p}\|^2
```