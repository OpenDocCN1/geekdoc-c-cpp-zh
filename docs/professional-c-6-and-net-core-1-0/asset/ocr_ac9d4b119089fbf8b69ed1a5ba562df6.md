```
<VisualState x:Name="PointerOver">
    <Storyboard>
        <ObjectAnimationUsingKeyFrames
            Storyboard.TargetProperty="BorderBrush"
            Storyboard.TargetName="ContentPresenter">
            <DiscreteObjectKeyFrame KeyTime="0"
                Value="{ThemeResource SystemControlHighlightBaseMediumLowBrush}"/>
        </ObjectAnimationUsingKeyFrames>
        <ObjectAnimationUsingKeyFrames
            Storyboard.TargetProperty="Foreground"
            Storyboard.TargetName="ContentPresenter">
            <DiscreteObjectKeyFrame KeyTime="0"
                Value="{ThemeResource SystemControlHighlightBaseHighBrush}"/>
        </ObjectAnimationUsingKeyFrames>
    </Storyboard>
</VisualState>
<VisualState x:Name="Pressed">
    <Storyboard>
        <!--animations removed-->
    </Storyboard>
</VisualState>
<VisualState x:Name="Disabled">
    <Storyboard>
        <!--animations removed-->
    </Storyboard>
</VisualState>
</VisualStateGroup>
</VisualStateManager.VisualStateGroups>
```

With WPF, the default button template retrieves resources for brushes using StaticResource and DynamicResource markup extensions because theme resources are not available here. The x.Static markup extension accesses static members of a class, here SystemColors.ControlTextBrushKey. The SystemColors class accesses resources that can be configured by the user, and thus the user can partially style the look. For the dynamic look when the mouse moves over the button, or the button is clicked, property triggers are used to change the look (code file TemplatesWPF/Styles/ControlTemplates.xaml):

```
<Style x:Key="ButtonStyle1" TargetType="{x:Type Button}">
    <Setter Property="FocusVisualStyle" Value="{StaticResource FocusVisual}"/>
    <Setter Property="Background"
        Value="{StaticResource Button.Static.Background}"/>
    <Setter Property="BorderBrush"
        Value="{StaticResource Button.Static.Border}"/>
    <Setter Property="Foreground"
        Value="{DynamicResource {x:Static SystemColors.ControlTextBrushKey}}"/>
    <Setter Property="BorderThickness" Value="1"/>
    <Setter Property="HorizontalContentAlignment" Value="Center"/>
    <Setter Property="VerticalContentAlignment" Value="Center"/>
    <Setter Property="Padding" Value="1"/>
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type Button}">
                <Border x:Name="border" BorderBrush="{TemplateBinding BorderBrush}"
```