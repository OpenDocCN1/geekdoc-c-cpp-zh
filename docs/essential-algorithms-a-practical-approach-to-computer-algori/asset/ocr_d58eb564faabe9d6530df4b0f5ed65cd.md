# Chapter 2 Numerical Algorithms

```
// Calculate the function at the endpoints and the midpoint.
Float: y1 = function(x1)
Float: y2 = function(x2)
Float: xm = (x1 + x2) / 2
Float: ym = function(xm)
```

```
// Calculate the area for the large slice and two subslices.
Float: area1 = (x2 - x1) * (y1 + y2) / 2.0
Float: arealm = (xm - x1) * (y1 + ym) / 2.0
Float: area2 = (x2 - xm) * (ym + y2) / 2.0
Float: arealm2 = area1 + area2
```

```
// See how close we are.
Float: error = (area2 - area1) / area1
```

```
// See if this is small enough.
If (Abs(error) < max_slice_error) Then Return arealm2
```

```
// The error is too big. Divide the slice and try again.
SliceArea(function, x1, xm, max_slice_error) +
SliceArea(function, xm, x2, max_slice_error)
SliceArea
```

If you run the AdaptivepointIntegration start with two initial slices, the program divides them into 24 slices shown in Figure 2-4 and estimates the area under the curve with -0.035%. If you use the TrapezoidRule program with 24 slices of uniform width, the program has an error of -0.072%, twice as much as that produced by the adaptive program. The two programs use the same number of slices, but the adaptive program positions them more effectively.

The AdaptiveTrapezoidIntegration sample program uses a different method to decide when to break a slice into slices. It calculates the second derivative of the function at the starting x value and divides the interval into one slice plus 1 per second derivative value. For example, if the second derivative is 2, the program divides the slice into three pieces (The formula for the number of slices chosen somewhat arbitrarily. You might get better results with a different formula.)

> In your case a bit rough, a derivative tells you the slope at any given point. Its second derivative tells you the slope's rate of change, or how fast the curve is bending. A higher second derivative means that the curve is bending relatively tightly, so the AdaptiveTrapezoidIntegration program uses more slices.

Of course, this technique won't work if you can't calculate the second derivative. The technique used by the AdaptiveMidpointIntegration seems to work fairly well in any case, so you can fall back on that technique.