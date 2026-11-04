# Part II: Application Development Using C#

You can also nest Canvas controls within one another. Edit the UI.xaml file created earlier and replace its content with the following:

```
<Canvas
xmlns="http://schemas.microsoft.com/client/2007"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" >

<Canvas
Canvas.Left="80" Canvas.Top="80"
Height="250" Width="250"
Background="lightgreen">

<Ellipse
Canvas.ZIndex="2"
Canvas.Left="10" Canvas.Top="10"
Height="200" Width="200"
Stroke="Black"
StrokeThickness="10"
Fill="Yellow" />

</Canvas>

</Canvas>
```

Reload the Default.html file in the web browser, and observe the changes (see Figure 19-6).

![](bbox=[0.38, 0.6, 0.62, 0.8])

Figure 19-6

> The positions specified by the Canvas.Left and Canvas.Top attributes of each element or control are relative to its parent control, and not the root control.