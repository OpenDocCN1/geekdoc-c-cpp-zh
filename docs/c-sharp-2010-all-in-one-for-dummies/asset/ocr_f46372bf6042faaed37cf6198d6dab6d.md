The Dock Panel also has a setting called LastChildFill. If this is true, the last element in XAML will fill the remaining real estate. Elements (prior to the last XAML element) that do not have a Dock setting specified will default to DockPanel.Dock="Left".

Figure 2-5:
Dock Panel.

![](bbox=[0.25, 0.28, 0.48, 0.5])

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

Well, it is ... most of the time. In some cases, part of your application needs to be laid out the "old way." A graphical application used to design floor plans is a perfect example.

Items are placed (or drawn) on the canvas relative to any side, and layering is handled through z-order. (See Figure 2-6 and Listing 2-5.)

Figure 2-6:
Canvas sample.

![](bbox=[0.27, 0.8, 0.45, 0.92])