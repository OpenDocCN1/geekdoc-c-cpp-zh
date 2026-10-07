The PathObjects example program shown in Figure 8-5 uses the following XAML code to draw two curves. The code first uses the Path mini-language to draw a curve and then draws the same curve by placing objects inside a Path control.

```
<!-- Draw using the Path mini-language. -->
<Path Stroke="Red" StrokeThickness="5">
<Path Data="60,20 Q140,150 150,140 0,30/100"/>

<!-- Draw using objects. -->
<Path Stroke="Red" StrokeThickness="5">
<Path.Data>
  <Geometry>
  <FigureCollection>
    <PathFigure>
      <PathFigure StartPoint="60,20">
      <Segments>
      <PathSegmentCollection>
        <QuadraticBezierSegment Points="140,150 150,140 0,30/100"/>
      </PathSegmentCollection>
      </Segments>
    </PathFigure>
  </FigureCollection>
  </Geometry>
</Path.Data>
</Path.>
</Path>
```

![](bbox=[0.615, 0.093, 0.872, 0.203])

The two methods produce the same output, but the Path mini-language is much simpler and more concise.

# POLYGON

The Polygon object draws lines that connect a series of points. It finishes by connecting the first point to the last point.

The following XAML code draws the polygon shown in the middle of Figure 8-2. The Points attribute at the end of the list contains the coordinates of the polygon that connects.

```
<Polygon Margin="15" HorizontalAlignment="Center" VerticalAlignment="Top" Width="Auto" Height="Auto" Fill="#FFF8B00" Stroke="#FF00000" StrokeThickness="5" Points="41,3 2,70 78,32 3,19 59,69//>
```

![](bbox=[0.715, 0.815, 0.872, 0.833])