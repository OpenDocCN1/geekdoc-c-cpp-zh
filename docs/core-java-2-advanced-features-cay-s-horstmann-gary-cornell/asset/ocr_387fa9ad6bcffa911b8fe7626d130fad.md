Coordinate transformations are very useful in practice. They allow you to work with convenient coordinate values. The graphics context takes care of the dirty work of transforming them to pixels.

There are four fundamental transformations.

+   - Scaling: blowing up, or shrinking, all distances from a fixed point
+   - Rotation: rotating all points around a fixed center
+   - Translation: moving all points by a fixed amount
+   - Shear: leaving one line fixed and “sliding” the lines parallel to it by an amount that is proportional to the distance from the fixed line

Figure 11.18 shows how these four fundamental transformations act on a unit square.

![](bbox=[0.217, 0.425, 0.867, 0.595])

**Figure 11.18** The fundamental transformations

The scale, rotate, translate, and shear methods of the Graphics2D class set the coordinate transformation of the graphics context to one of these fundamental transformations.

You can compose the transformations. For example, you might want to rotate shapes and double their size; supply both a rotation and a scaling transformation:

```
g2.rotate(angle);
g2.scale(2, 2);
g2.draw(...);
```

In this case, it does not matter in which order you supply the transformations. However, with most transformations, order does matter. For example, if you want to rotate and shear, then it makes a difference which of the transformations you supply first. You need to figure out what your intention is. The graphics