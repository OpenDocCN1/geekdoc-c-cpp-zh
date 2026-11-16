Then, the y and z components are the subscripts rotated in the order x → y → z → x, yielding the next two components of the cross product result:

```
c_y = a_z b_x - a_x b_z
c_z = a_x b_y - a_y b_x
```

As with the dot product, there's a special case to consider. If the cross product returns the vector <o,o,o>, this means that a⃗ and b⃗ are collinear. Two collinear vectors cannot form a plane, and therefore there's no normal for the cross product to return.

Because a triangle lies on a single plane, the cross product can determine the normal of the triangle. Figure 3.10 shows triangle ABC. To calculate the normal, first construct two vectors for edges of the triangle:

```
u⃗ = B - A
v⃗ = C - A
```

![](bbox=[0.27, 0.605, 0.6, 0.795])

Figure 3.10 Normal to triangle ABC

Then take the cross product between these two vectors