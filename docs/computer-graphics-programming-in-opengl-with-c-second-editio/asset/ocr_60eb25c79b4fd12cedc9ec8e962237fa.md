Then, a point \(P_M\) in its own model space is transformed directly to camera space in one step as follows:

```
$$P_C = MV * P_M$$
```

The advantage of this approach becomes clear when one considers that, in a complex scene, we will need to perform this transformation not on just one point, but on *every vertex in the scene*. By pre-computing MV, transforming each point into view space will require us to do just *one* matrix multiplication per vertex, rather than two. Later, we will see that we can extend this process to pre-computing several matrix concatenations, reducing the per-vertex computations considerably.

# ### 3.3 PROJECTION MATRICES

Now that we have established the camera, we can examine *projection matrices*. Two important projection matrices that we will now examine are (a) *perspective* and (b) *orthographic*.

# ### 3.3.1 The Perspective Projection Matrix

Perspective projection attempts to make a 2D picture appear 3D, by utilizing the concept of perspective to mimic what we see when we look at the real world. Objects that are close appear larger than objects that are far away, and in some cases, lines that are parallel in 3D space are no longer parallel when drawn with perspective.

Perspective was one of the great discoveries of the Renaissance era in the 1400–1500s, when artists started painting with more realism than did their predecessors.

An excellent example can be seen in Figure 3.14, “The Annunciation, with Saint Emidius” by Carlo Crivelli, painted in 1486 (currently held at the National Gallery in London [CR86]). The intense use of perspective is clear—the receding lines of the left-facing wall of the building on the right are slanted toward each other dramatically. This creates the illusion of depth and 3D space, and in the process lines that are parallel in reality are not parallel in the picture. Also, the people in the foreground are larger than the people in the background. While today we take these devices for granted, finding a transformation matrix to accomplish this requires some mathematical analysis.