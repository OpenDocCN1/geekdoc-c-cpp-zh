# Modified ScrollBar 55

```
<Track.Thumb>
  <Thumb Background="Blue" />
</Track.Thumb>
<Track>
<RepeatButton Name="btnSmallUp" Grid.Column="2"
  Command="ScrollBar.LineRightCommand">
<Path HorizontalAlignment="Center" VerticalAlignment="Center"
  Data="M2,3 L10,3 L6,7" Stroke="Blue" StrokeThickness="3"
StrokeStartCap="Round" StrokeEndLineCap="Round"/>n</RepeatButton>
</Grid>
<ControlTemplate.Triggers>
  Triggers ... 
</ControlTemplate.Triggers>
</ControlTemplate>
```

![](bbox=[0.788, 0.335, 0.941, 0.355])

The template's Triggers change the locations of the components in the Grid depending on the control's orientation property. They also set the RepeatButtons Command for the Left/Right commands or the Up/Down commands. To save, the Triggers section isn't shown here. Download the example program to see the full code.

You could add other Triggers such as one to change the control's appearance when its IsEnabled property is False.

The BareBonesScrollBar example program demonstrates this template.

# MODIFIED SCROLLBAR

The ScrollBar template described in the previous section makes a ScrollBar that looks like it's made up of a bunch of buttons (which it is). The following template gives a scrollbar more distinct appearance:

```
<ControlTemplate x:Key="tempScrollBar" TargetType="ScrollBar">
<ControlTemplate.Resources>
<ControlTemplate x:Key="tempSmallChangeButtons" TargetType="RepeatButton">
<Grid>
  <Ellipse Fill="Blue" Height="12" MinWidth="10"/>
<ContentPresenter/>
</Grid>
</ControlTemplate>
<ControlTemplate x:Key="tempChangeButtonsH" TargetType="RepeatButton">
<Grid>
  <Grid.RowDefinitions>
    <RowDefinition Height="*"/>
    <RowDefinition Height="2"/>
    <RowDefinition Height="*"/>
  </Grid.RowDefinitions>
  <Rectangle Grid.Row="1" Radius="10" RadiusY="10"
    Fill="SkyBlue"/>
<ContentPresenter/>
</Grid>
</ControlTemplate>
</ControlTemplate>
```

![](bbox=[0.078, 0.665, 0.158, 0.735])