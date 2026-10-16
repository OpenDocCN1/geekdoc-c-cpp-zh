```
<Style x:Key="ButtonStyle1" TargetType="Button">
    <Setter Property="Background"
        Value="{ThemeResource SystemControlBackgroundBaseLowBrush}"/>
    <Setter Property="Foreground"
        Value="{ThemeResource SystemControlForegroundBaseHighBrush}"/>
    <Setter Property="BorderBrush"
        Value="{ThemeResource SystemControlForegroundTransparentBrush}"/>
    <Setter Property="BorderThickness"
        Value="{ThemeResource ButtonBorderThemeThickness}"/>
    <Setter Property="Padding" Value="8,4,8,4"/>
    <Setter Property="HorizontalAlignment" Value="Left"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="FontFamily"
        Value="{ThemeResource ContentControlThemeFontFamily}"/>
    <Setter Property="FontWeight" Value="Normal"/>
    <Setter Property="FontSize"
        Value="{ThemeResource ControlContentThemeFontSize}"/>
    <Setter Property="UseSystemFocusVisuals" Value="True"/>
```

The template of the control consists of a Grid and a ContentPresenter where values for brushes and borders are bound using TemplateBinding. This way it is possible to define these values directly with the Button control to influence the look.

```
<Setter Property="Template">
    <Setter.Value>
        <ControlTemplate TargetType="Button">
            <Grid x:Name="RootGrid" Background="{TemplateBinding Background}">
                <!--Visual State Manager settings removed-->
                <ContentPresenter x:Name="ContentPresenter"
                    AutomationProperties.AccessibilityView="Raw"
                    BorderBrush="{TemplateBinding BorderBrush}"
                    BorderThickness="{TemplateBinding BorderThickness}"
                    ContentTemplate="{TemplateBinding ContentTemplate}"
                    ContentTransitions="{TemplateBinding ContentTransitions}"
                    Content="{TemplateBinding Content}"
                    HorizontalContentAlignment="
                        "{TemplateBinding HorizontalContentAlignment}"
                    Padding="{TemplateBinding Padding}"
                    VerticalContentAlignment=
                        "{TemplateBinding VerticalContentAlignment}"/>
            </Grid>
        </ControlTemplate>
    </Setter.Value>
</Setter>
</Style>
```

For dynamic button changes, if the mouse moves over the button, or the button is pressed, the UWP app template for the button makes use of the VisualStateManager. Here, key-frame animations are defined when the button changes to the states PointerOver, Pressed, and Disabled:

```
<VisualStateManager.VisualStateGroups>
    <VisualStateGroup x:Name="CommonStates">
        <VisualState x:Name="Normal"/>
```