# # HOW'D YOU DO?

It doesn't matter if your button is a little different from mine, as long as it works and you're happy with it. (Oh, and changing the BorderBrush? It does nothing. Keep reading to find out why.)

```
<Window.Resources>
<LinearGradientBrush x:Key="BackgroundGradient" EndPoint="0.5,1" StartPoint="0.5,0">
<GradientStop Color="#FF000000" Offset="0.483"/>
<GradientStop Color="#FFFFFFFF" Offset="1"/>
<GradientStop Color="#FF0E0E0E" Offset="0"/>
</LinearGradientBrush>
<RadialGradientBrush x:Key="CenterGradient" GradientOrigin="0.5,0.5">
<GradientStop Color="#FF3F369F" Offset="1"/>
<GradientStop Color="#FF1E1A49" Offset="0"/>
</RadialGradientBrush>
<LinearGradientBrush x:Key="HighlightGradient" EndPoint="0.5,1" StartPoint="0.5,0">
<GradientStop Offset="1"/>
<GradientStop Color="#FFFFFFF" Offset="0"/>
<GradientStop Color="#52FFFFFF" Offset="0.409"/>
</LinearGradientBrush>
</Window.Resources>
```

The definition of the brushes hasn't changed (I've just moved them to the Window so that they can be referenced by both buttons.

Except for the Resources section, which I moved to the Window, the first button is identical to the example.

```
<Grid>
<Grid.ColumnDefinitions ... >
<Button Grid.Column="1" Width="200" Height="200" VerticalAlignment="Center" HorizontalAlignment="Center">
<Button.Template>
<ControlTemplate>
<Border x:Name="RoundedRectBorder" CornerRadius="15" Margin="15" Background="{StaticResource BackgroundGradient}" BorderThickness="0.75" BorderBrush="Black">
<Rectangle x:Name="RectCenter" Margin="15" Fill="{StaticResource CenterGradient}" />
<Rectangle x:Name="RectHighlight" Margin="15,15,15,75" Fill="{StaticResource HighlightGradient}" Opacity="0.75"/>
</Border>
</ControlTemplate>
</Button.Template>
</Button>
</Grid>
```

The only real change here is swapping Rectangle shapes for the Ellipse shapes in the first version.