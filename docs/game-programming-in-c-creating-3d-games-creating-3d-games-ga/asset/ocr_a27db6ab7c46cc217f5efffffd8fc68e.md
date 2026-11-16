The distance of this new line segment is the minimal distance between C and AB. To figure out this line segment, you first need to compute the vector p.

You already know the direction of p, as it's in the same direction as the normalized AB. To figure out the distance of p, you apply a property of the dot product called the scalar projection. Given a unit vector and a non-unit vector, extend (or contract) the unit vector such that a right triangle forms with the non-unit vector. The dot product then returns the length of this extended unit vector.

In this example, the length of p is the dot product between AC and a normalized AB:

```
$$ \|\vec{p}\| = \overrightarrow{AC} \cdot \frac{\overrightarrow{AB}}{\|\overrightarrow{AB}\|} $$
```

```
$$ \left\| \vec{p} \right\| = \overrightarrow{AC} \cdot \frac{\overrightarrow{AB}}{\|\overrightarrow{AB}\|} $$
```

The vector p is then the scalar multiplication between the length of p and the normalized AB:

```
$$ \vec{p} = \|\vec{p}\| \frac{\overrightarrow{AB}}{\|\overrightarrow{AB}\|} $$
```

```
$$ \vec{p} = \|\vec{p}\| \cdot \frac{\overrightarrow{AB}}{\|\overrightarrow{AB}\|} $$
```

Using some algebraic manipulation—and remembering that the length squared of a vector is the same as a dot