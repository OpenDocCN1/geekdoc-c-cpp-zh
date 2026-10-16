to 0.5.

The second ellipse, `GelShine`, is a small ellipse whose size is defined by the `Margin` property and so is visible within the first ellipse. The stroke is transparent, so there is no line surrounding the ellipse. This ellipse uses a linear gradient fill brush, which transitions from a light, partly transparent color to full transparency. This gives the ellipse a shimmering effect (code file `Templates[WPF|UWP]/Styles/ControlTemplates.xaml`):

```
```xml
<ResourceDictionary
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
    <Style x:Key="RoundedGelButton" TargetType="Button">
        <Setter Property="Width" Value="100" />
        <Setter Property="Height" Value="100" />
        <Setter Property="Foreground" Value="White" />
        <Setter Property="Template">
            <Setter.Value>
                <ControlTemplate TargetType="Button">
                    <Grid>
                        <Ellipse Name="GelBackground" StrokeThickness="0.5"
                                 Fill="Black">
                            <Ellipse.Stroke>
                                <LinearGradientBrush StartPoint="0,0"
                                                      EndPoint="0,1">
                                    <GradientStop Offset="0" Color="#ff7e7e7e" />
                                    <GradientStop Offset="1" Color="Black" />
                                </LinearGradientBrush>
                            </Ellipse.Stroke>
                        </Ellipse>
                        <Ellipse Margin="15,5,15,50">
                            <Ellipse.Fill>
                                <LinearGradientBrush StartPoint="0,0"
                                                      EndPoint="0,1">
                                    <GradientStop Offset="0" Color="#aaffffff" />
                                    <GradientStop Offset="1" Color="Transparent"
                                    />
                                </LinearGradientBrush>
                            </Ellipse.Fill>
                        </Ellipse>
                    </Grid>
                </ControlTemplate>
            </Setter.Value>
        </Setter>
    </Style>
</ResourceDictionary>
```
```

From the `app.xaml` file, the resource dictionary is referenced as shown here (code file `Templates[WPF|UWP]/App.xaml`):

```
```xml
<Application x:Class="TemplateDemo.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    StartupUri="MainWindow.xaml">
    <Application.Resources>
        <ResourceDictionary Source="Styles/ControlTemplates.xaml" />
    </Application.Resources>
</Application>
```
```