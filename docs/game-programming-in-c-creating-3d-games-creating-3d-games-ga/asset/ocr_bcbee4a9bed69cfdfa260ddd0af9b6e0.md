\( A' \)
\( =((-2+5)\cos90^\circ + 1\sin90^\circ ,\)
\( (-2+5)\sin90^\circ - 1\cos90^\circ) = (1,3) \)
\( B' = (5\cos90^\circ - 1\sin90^\circ, 5\sin90^\circ + 1\cos90^\circ) \)
\( = (-1,5) \)
\( C' \)
\( =((2+5)\cos90^\circ + 1\sin90^\circ, (2+5)\sin90^\circ - 1\cos90^\circ) \)
\( = (1,7) \)

In the case of translation first, rotation second, you end up with a triangle still facing to the left but positioned several units above the origin, as in Figure 5.5(c). This happens because you first move the triangle to the right, and then you rotate about the origin. Usually, this behavior is undesirable.

![](bbox=[0.16, 0.52, 0.72, 0.66])

Figure 5.5 (a) Initial triangle, (b) rotating then translating, and (c) translating then rotating

Because the order of transformations matter, it's important to have a consistent order. For the transformation from object space to world space, always apply the transformations in the order scale, then rotation, then translation. Keeping this in mind, you