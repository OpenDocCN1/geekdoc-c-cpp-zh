+   - The `GradientPaint` class varies colors by interpolating between two given color values (see Figure 11.45).

![](bbox=[0.356, 0.197, 0.556, 0.34])

**Figure 11.45** Gradient paint

+   - The `TexturePaint` class fills an area with repetitions of an image (see Figure 11.46).

![](bbox=[0.357, 0.452, 0.556, 0.592])

**Figure 11.46** Texture paint

You can construct a `GradientPaint` object by specifying two points and the colors that you want at these two points.

```
`g2.setPaint(new GradientPaint(p1, Color.RED, p2, Color.YELLOW));`
```

Colors are interpolated along the line joining the two points. Colors are constant along lines perpendicular to that joining line. Points beyond an end point of the line are given the color at the end point.

Alternatively, if you call the `GradientPaint` constructor with true for the cyclic parameter:

```
`g2.setPaint(new GradientPaint(p1, Color.RED, p2, Color.YELLOW, true));`
```

Then, the color variation cycles and keeps varying beyond the end points.