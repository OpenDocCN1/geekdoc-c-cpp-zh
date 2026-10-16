combines an `EllipseGeometry` and a `RectangleGeometry` to form a union, as shown in Figure 30.5.

![](bbox=[0.105, 0.105, 0.895, 0.162])

# Figure 30.5

```
<Path Canvas.Top="0" Canvas.Left="250" Fill="Blue" Stroke="Black" >
    <Path.Data>
        <CombinedGeometry GeometryCombineMode="Union">
            <CombinedGeometry.Geometry1>
                <EllipseGeometry Center="80,60" RadiusX="80" RadiusY="40" />
            </CombinedGeometry.Geometry1>
            <CombinedGeometry.Geometry2>
                <RectangleGeometry Rect="30,60 105 50" />
            </CombinedGeometry.Geometry2>
        </CombinedGeometry>
    </Path.Data>
</Path>
```

Figure 30.5 shows this XAML code in different variants—from left to right, `Union`, `Xor`, `Intersect`, and `Exclude`.

# Transformation

Because XAML is vector based, you can resize every element. In the next example, the vector-based graphics are now scaled, rotated, and skewed. Hit testing (for example, with mouse moves and mouse clicks) still works but without the need for manual position calculation.

Figure 30.6 shows a rectangle in several different forms. All the rectangles are positioned within a `StackPanel` element with horizontal orientation to have the rectangles one beside the other. The first rectangle has its original size and layout. The second one is resized, the third moved, the forth rotated, the fifth skewed, the sixth transformed using a transformation group, and the seventh transformed using a matrix. The following sections get into the code samples of all these options.

![](bbox=[0.105, 0.735, 0.895, 0.865])

# Figure 30.6

# Scaling