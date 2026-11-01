```
<Setter Property="FontSize" Value="18" />
<Setter Property="FontFamily" Value="arial" />
<Setter Property="FontWeight" Value="bold" />
```

Next, the Button.Foreground property is set using property element syntax because a brush is used:

```
<Setter Property="Foreground">
    <Setter.Value>
        <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">
            <LinearGradientBrush.GradientStops>
                <GradientStop Offset="0.0" Color="Purple" />
                <GradientStop Offset="0.5" Color="Azure" />
                <GradientStop Offset="1.0" Color="Purple" />
            </LinearGradientBrush.GradientStops>
        </LinearGradientBrush>
    </Setter.Value>
</Setter>
```

The remainder of the code for the Style object sets the Button.Template property to a ControlTemplate object:

```
<Setter Property="Template">
    <Setter.Value>
        <ControlTemplate TargetType="Button">
            ...
        </ControlTemplate>
    </Setter.Value>
</Setter>
</Style>
</Button.Style>
</Button>
```

The template code can be summarized as a Grid control that contains three cells in a single row. In turn, these cells contain an Ellipse, a Rectangle, the ContentPresenter for the template, and another Ellipse:

```
<Grid>
    <Ellipse Grid.Column="0" Height="50">
        ...
    </Ellipse>
    <Grid Grid.Column="1">
        <Rectangle RadiusX="10" RadiusY="10">
            ...
        </Rectangle>
        <ContentPresenter Margin="20,0,20,0"
            HorizontalAlignment="Center"
            VerticalAlignment="Center" />
    </Grid>
    <Ellipse Grid.Column="2" Height="50">
        ...
    </Ellipse>
</Grid>
```