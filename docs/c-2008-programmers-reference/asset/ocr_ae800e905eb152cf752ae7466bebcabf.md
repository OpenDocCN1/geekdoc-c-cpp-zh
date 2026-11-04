# ### Using SolidColorBrush

The `<SolidColorBrush>` element paints an area with a solid color. Edit the `UI.xaml` file created in the previous section, and replace its content with the following:

```
~~~xml
<Canvas
    xmlns="http://schemas.microsoft.com/client/2007"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">

  <Ellipse
    Canvas.Left="10" Canvas.Top="10"
    Height="100" Width="100"
    Stroke="Black"
    StrokeThickness="10"
    Fill="Yellow" />

  <Ellipse
    Canvas.Left="120" Canvas.Top="10"
    Height="100" Width="100"
    Stroke="Black"
    StrokeThickness="10"
    Fill="#A3FC96" /> <!-- 6-digit hexadecimal -->

  <Ellipse
    Canvas.Left="10" Canvas.Top="120"
    Height="100" Width="100"
    Stroke="Black"
    StrokeThickness="10"
    Fill="#A3FC96FF" />
  <!-- 6-digit hexadecimal + 2-digit for alpha/opacity value -->

  <Ellipse
    Canvas.Left="120" Canvas.Top="120"
    Height="100" Width="100"
    Stroke="Black"
    StrokeThickness="10">
    <Ellipse.Fill>
      <SolidColorBrush Color="LightBlue"/>
    </Ellipse.Fill>
  </Ellipse>

</Canvas>
~~~
```

In this example, the `Fill` attribute specifies the solid color to use to fill up the particular element. Reload the `Default.html` file in the web browser, and observe the output in your browser (see Figure 19-12).

![](bbox=[0.416, 0.777, 0.66, 0.922])

**Figure 19-12**