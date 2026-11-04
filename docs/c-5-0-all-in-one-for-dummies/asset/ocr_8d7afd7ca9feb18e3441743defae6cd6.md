![](bbox=[0.24, 0.17, 0.42, 0.38])

Figure 2-5:
Dock Panel.

# Listing 2-4: Dock Panel XAML

```
<DockPanel LastChildFill="True">
    <Button DockPanel.Dock="Left" Content="Far Left"/>
    <Button DockPanel.Dock="Left" Content="Near Left"/>
    <Button DockPanel.Dock="Top" Content="Top"/>
    <Button DockPanel.Dock="Bottom" Content="Bottom"/>
    <Button Content="Fill"/>
    <Button Content="Fill More"/>
</DockPanel>
```

# Canvas

The Canvas is a bit of an anomaly in WPF, since it doesn't use flow layout, but goes back to fix position layout rendering. "What?!" you say. "I thought flow layout was the way of the future!"

Well, it is . . . most of the time. In some cases, part of your application needs to be laid out the "old way." A graphical application used to design floor plans is a perfect example.

Items are placed (or drawn) on the canvas relative to any side, and layering is handled through z-order. (See Figure 2-6 and Listing 2-5.)

![](bbox=[0.24, 0.75, 0.42, 0.88])

Figure 2-6:
Canvas sample.

# Listing 2-5: Canvas XAML

```
<Canvas>
    <Rectangle Canvas.Left="40" Canvas.Top="40" Height="53" Name="rectangle1" Stroke="Black" Width="96" Fill="#FFEE2323" />
```