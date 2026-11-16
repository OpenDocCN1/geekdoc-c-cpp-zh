the width of the view, the height of the view, the distance to the near plane, and the distance to the far plane. Given these parameters, this is the orthographic projection matrix:

```
Orthographic = [
  2/width   0         0         0
  0         2/height  0         0
  0         0         1/(far-near) 0
  0         0         near/(near-far) 1
]
```

```
Orthographic = [
  2/width   0         0         0
  0         2/height  0         0
  0         0         1/(far-near) 0
  0         0         near/(near-far) 1
]
```

Note that this orthographic projection matrix is like the SimpleViewProjection matrix in Chapter 5, except there are additional terms accounting for the near and far planes.

The perspective projection has an additional parameter called the horizontal field of view (FOV). This is the horizontal angle around the camera that’s visible in the projection. Changing the field of view determines how much of the 3D world is visible. This is the perspective matrix: