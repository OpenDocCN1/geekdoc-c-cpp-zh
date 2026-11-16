# Infinite Lines

Table 7.3.4 shows the infinite line components.

| Name | Math Notation | Type |
|---|---|---|
| Point on Line | L_point | Vector |
| Direction | L_dir | Vector |

Infinite lines are just that—lines that go on forever. To store them, you only need to keep track of a single point on the line and the direction the line is going in (Table 7.3.4). To calculate the audio position, you need to orthogonally project the listener's location onto the line. Don't worry if that scares you as it's very simple to do. Just remember that you must use the same point on the line throughout the equation otherwise the audio position will be created in the wrong place!

The closest-point equation for an infinite line is presented in Equation 7.3.2.

```
V = X - L_point
d = V . L_dir
A = L_point + L_dir d
(7.3.2)
```

It is created by the following steps:

+   1. Create a vector between the listener and any point on the line.
+   2. Take the dot product between this vector and the direction of the line. This will tell us how far along the line to create the new point from the test point.
+   3. Set the new audio location by scaling the direction by the distance and adding it to the point on the line used in step 1.

# Line Segments

Table 7.3.5 shows the line segment components.

| Name | Math Notation | Type |
|---|---|---|
| Origin | L_origin | Vector |
| Direction | L_dir | Vector |
| Length | L_length | Scalar |