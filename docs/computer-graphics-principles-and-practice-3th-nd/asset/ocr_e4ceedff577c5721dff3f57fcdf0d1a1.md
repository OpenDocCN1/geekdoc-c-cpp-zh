# # 10.9 Another Example of Building a 2D Transformation

Suppose we want to find a 3 × 3 matrix transformation that rotates the entire plane 30° counterclockwise around the point P = (2, 4), as shown in Figure 10.14. As you’ll recall, WPF expresses this transformation via code like this:

```
```xml
<RotateTransform Angle="-30" CenterX="2" CenterY="4"/>
```
```

An implementer of WPF then must create a matrix like the one we're about to build.

Here are two approaches.

First, we know how to rotate about the origin by 30°; we can use the transformation T1 from the start of the chapter. So we can do our desired transformation in three steps (see Figure 10.15).

+   1. Move the point (2, 4) to the origin.
+   2. Rotate by 30°.
+   3. Move the origin back to (2, 4).

The matrix that moves the point (2, 4) to the origin is

```
```text
[ 1  0 -2 ]
[ 0  1 -4 ]
[ 0  0  1 ]        (10.74)
```
```

The one that moves it back is similar, except that the 2 and 4 are not negated. And the rotation matrix (expressed in our new 3 × 3 format) is

```
```text
[ cos 30°  -sin 30°   0 ]
[ sin 30°   cos 30°   0 ]
[   0         0       1 ]        (10.75)
```
```

The matrix representing the entire sequence of transformations is therefore

```
```text
[ 1  0  2 ] [ cos 30°  -sin 30°   0 ] [ 1  0 -2 ]
[ 0  1  4 ] [ sin 30°   cos 30°   0 ] [ 0  1 -4 ]
[ 0  0  1 ] [   0         0       1 ] [ 0  0  1 ]        (10.76)
```
```

> > **Inline Exercise 10.18:** (a) Explain why this is the correct order in which to multiply the transformations to get the desired result.
> > (b) Verify that the point (2, 4) is indeed left unmoved by multiplying [2 4 1]^T by the sequence of matrices above.

The second approach is again more automatic: We find three points whose target locations we know, just as we did with the windowing transformation above. We’ll use P = (2, 4), Q = (3, 4) (the point one unit to the right of P), and R = (2, 5) (the point one unit above P). We know that we want P sent to P, Q sent to (2 + cos 30°, 4 + sin 30°), and R sent to (2 − sin 30°, 4 + cos 30°). (Draw a picture to convince yourself that these are correct.) The matrix that achieves this is just

![](bbox=[0.72, 0.147, 0.958, 0.381])

*Figure 10.14:* We'd like to rotate the entire plane by 30° counter-clockwise about the point P = (2, 4).