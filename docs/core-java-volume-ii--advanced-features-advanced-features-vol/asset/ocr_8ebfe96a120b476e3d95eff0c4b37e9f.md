Such a transformation is called an *affine transformation*. In the Java 2D API, the `AffineTransform` class describes such a transformation. If you know the components of a particular transformation matrix, you can construct it directly as

```
```
var t = new AffineTransform(a, b, c, d, e, f);
```
```

Additionally, the factory methods `getRotateInstance`, `getScaleInstance`, `getTranslateInstance`, and `getShearInstance` construct the matrices that represent these transformation types. For example, the call

```
```
t = AffineTransform.getScaleInstance(2.0F, 0.5F);
```
```

returns a transformation that corresponds to the matrix

```
```
[ 2    0    0 ]
[ 0   0.5   0 ]
[ 0    0    1 ]
```
```

Finally, the instance methods `setToRotation`, `setToScale`, `setToTranslation`, and `setToShear` set a transformation object to a new type. Here is an example:

```
```
t.setToRotation(angle); // sets t to a rotation
```
```

You can set the coordinate transformation of the graphics context to an `AffineTransform` object.

```
```
g2.setTransform(t); // replaces current transformation
```
```

However, in practice, you shouldn’t call the `setTransform` operation, as it replaces any existing transformation that the graphics context may have. For example, a graphics context for printing in landscape mode already contains a 90-degree rotation transformation. If you call `setTransform`, you obliterate that rotation. Instead, call the `transform` method.

```
```
g2.transform(t); // composes current transformation with t
```
```

It composes the existing transformation with the new `AffineTransform` object.

If you just want to apply a transformation temporarily, first get the old transformation, compose it with your new transformation, and finally restore the old transformation when you are done.

```
```
AffineTransform oldTransform = g2.getTransform(); // save old transform
g2.transform(t); // apply temporary transform
draw on g2
g2.setTransform(oldTransform); // restore old transform
```
```