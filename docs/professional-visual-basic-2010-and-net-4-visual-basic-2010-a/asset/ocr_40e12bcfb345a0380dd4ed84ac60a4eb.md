```
</ControlTemplate>
    </Setter.Value>
</Setter>
</Style>
<LinearGradientBrush x:Key="ButtonNormalBackground" EndPoint="0,1" StartPoint="0,0">
    <GradientStop Color="#F3F3F3" Offset="0"/>
    <GradientStop Color="#EBEBEB" Offset="0.5"/>
    <GradientStop Color="#DDDDDD" Offset="0.5"/>
    <GradientStop Color="#CDCDCD" Offset="1"/>
</LinearGradientBrush>
<SolidColorBrush x:Key="ButtonNormalBorder" Color="#FF707070"/>
<Style x:Key="ButtonStyle1" TargetType="{x:Type Button}">
    <Setter Property="FocusVisualStyle" Value="{StaticResource ButtonFocusVisual}"/>
    <Setter Property="Background" Value="{StaticResource ButtonNormalBackground}"/>
    <Setter Property="BorderBrush" Value="{StaticResource ButtonNormalBorder}"/>
    <Setter Property="BorderThickness" Value="1"/>
    <Setter Property="Foreground" Value="{DynamicResource {x:Static SystemColors.ControlTextBrushKey}}"/>
    <Setter Property="HorizontalContentAlignment" Value="Center"/>
    <Setter Property="VerticalContentAlignment" Value="Center"/>
    <Setter Property="Padding" Value="1"/>
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type Button}">
                <Microsoft_Windows_Themes:ButtonChrome SnapsToDevicePixels="true" x:Name="Chrome" Background="{TemplateBinding Background}" BorderBrush="{TemplateBinding BorderBrush}" RenderDefaulted="{TemplateBinding IsDefaulted}" RenderMouseOver="{TemplateBinding IsMouseOver}" RenderPressed="{TemplateBinding IsPressed}">
                    <ContentPresenter SnapsToDevicePixels="{TemplateBinding SnapsToDevicePixels}" HorizontalAlignment="{TemplateBinding HorizontalContentAlignment}" Margin="{TemplateBinding Padding}" VerticalAlignment="{TemplateBinding VerticalContentAlignment}" RecognizesAccessKey="True"/>
                </Microsoft_Windows_Themes:ButtonChrome>
                <ControlTemplate.Triggers>
                    <Trigger Property="IsKeyboardFocused" Value="true">
                        <Setter Property="RenderDefaulted" TargetName="Chrome" Value="true"/>
                    </Trigger>
                    <Trigger Property="ToggleButton.IsChecked" Value="true">
                        <Setter Property="RenderPressed" TargetName="Chrome" Value="true"/>
                    </Trigger>
                    <Trigger Property="IsEnabled" Value="false">
                        <Setter Property="Foreground" Value="#ADADAD"/>
                    </Trigger>
                </ControlTemplate.Triggers>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```

There are two lines of interest in the preceding code block. The first concerns the actual button style defined. Styles often reference other resources; and similar to early C compilers, references must be defined before they are actually referenced. Thus, the style defined in the preceding code block is actually the last style entry:

    <Style x:Key="ButtonStyle1" TargetType="{x:Type Button}">

This line, which is highlighted in bold in the code block, indicates that this set of resources defines a style with the key ButtonStyle1. Because this style is defined with a key, it is not a default style applied to all controls of the target type. Styles always define a target type because different control types expect different specific values defined within all of the detailed elements of a style.