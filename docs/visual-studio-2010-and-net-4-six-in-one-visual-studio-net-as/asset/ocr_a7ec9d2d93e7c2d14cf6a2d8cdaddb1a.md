![](bbox=[0.104, 0.115, 0.143, 0.153])

```
<UserControl x:Class="Templateemos.ButtonTemplating"
xmlns="http://schemas.microsoft.com/winfx/2006/xml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="400">
<UserControl.Resources>
  <ControlTemplate x:Key="ButtonControlTemplate" TargetType="Button">
    <Grid>
      <Ellipse Fill="White" Stroke="Black"/>
      <ContentPresenter Margin="10" Content="{TemplateBinding Content}"/>
    </Grid>
  </ControlTemplate>
</UserControl.Resources>
<Grid x:Name="Layout" Background="White">
  <Button Content="Button" HorizontalAlignment="Center"
VerticalAlignment="Center"
Template="{StaticResource ButtonTemplate}" />
  <Button Content="Button with loong text" HorizontalAlignment="Center"
VerticalAlignment="Center" Template="{StaticResource ButtonControlTemplate}"
Margin="0.79,0,0,0" / "0" />
</Grid>
</UserControl>
```

Code file [ButtonTemplating.xaml] available for download at Wrox.com

The ControlTemplate is stored as a resource; it can be moved to an external resource dictionary. The template itself is very simple. It contains of a Grid, and an Ellipse that fills the grid, and a ContentPresenter that uses TemplateBinding to bind to the Content property of the Button. This technique can be used to use the internals of a control to change the settings and properties that the control's (the developer or designer) sets.

![](bbox=[0.738, 0.715, 0.912, 0.778])

FIGURE 8-19: Templating a Button

Even though the entire tree has been completely replaced, the new Button works as expected. Click events (as they should), but there is no visual indicator of clicking the mouse, or hovering over the Button.

To allow complete separation between logic and appearance, Silverlight introduced the concept of virtual states, which are basically sets of changes to the properties within the template, controlled