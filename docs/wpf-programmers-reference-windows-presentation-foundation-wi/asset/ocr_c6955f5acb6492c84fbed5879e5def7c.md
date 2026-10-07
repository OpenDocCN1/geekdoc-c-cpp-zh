# Building Complex Scenes | 403

The BarChart and Graph example programs shown in Figures 23-11 and 23-12, respectively, use the same MakeRectangle routine described earlier to draw bar charts and ribbon graphs.

![](bbox=[0.152, 0.151, 0.485, 0.396])

![](bbox=[0.608, 0.151, 0.952, 0.396])

FIGURE 23-11

FIGURE 23-12

These two programs only add a few techniques to those described earlier. Both of these programs color their rectangles with a material that uses a linear gradient brush that shades from the bottom to the top. For example, the following code shows how the Graph program builds its material:

```
Dim graph_brush As New LinearGradientBrush()
graph_brush.StartPoint = New Point(0, 0)
graph_brush.EndPoint = New Point(0, 1)
graph_brush.GradientStops.Add(New GradientStop(Colors.Blue, 0.0))
graph_brush.GradientStops.Add(New GradientStop(Colors.Lime, 0.25))
graph_brush.GradientStops.Add(New GradientStop(Colors.Yellow, 0.5))
graph_brush.GradientStops.Add(New GradientStop(Colors.Orange, 0.75))
graph_brush.GradientStops.Add(New GradientStop(Colors.Red, 1.0))
Dim graph_material As New DiffuseMaterial(graph_brush)
```

![](bbox=[0.152, 0.523, 0.952, 0.68])

The programs use this material to shade all of the rectangles they draw, setting each point's texture coordinates to a value that depends on its Y. For example, a point with Y coordinate 0 gets texture coordinates with second component 0. That gives the point the color of the gradient brush — blue.

Other coordinates are scaled so that the largest Y values in the data are given texture coordinates closest to 1; thus, they get colors near the end of the brush — red.

The top and bottom of the bars drawn by the BarChart program have texture coordinates set to the appropriate scaled Y, so the bottoms are blue and the tops depend on the bars' heights.

You could directly determine where to create each triangle in these figures, but the MakeRectangle routine makes things a lot easier.