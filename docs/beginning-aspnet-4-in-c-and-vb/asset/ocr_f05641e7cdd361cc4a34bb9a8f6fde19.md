```
NavigateUri="/About" TargetName="ContentFrame"
Content="about"/>

</StackPanel>
</Border>
</Grid>
```

The Welcome page is shown with loading the Silverlight control because it is referenced directly with the Source property from the Frame element. This Page just contains a TextBlock element with information about the application, which is contained within a Border element for defining some visual effects that is contained within a Canvas element for positioning.

```
<navigation:Page x:Class="Wrox.ProCSharp.Silverlight.Views.Welcome"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:navigation="clr-namespace:System.Windows.Controls.Navigation;
assembly=System.Windows.Controls.Navigation"
Title="Welcome Page">
<Canvas x:Name="LayoutRoot">
<Canvas.Resources>
<!-- Storyboard Resources -->
</Canvas.Resources>
<Border x:Name="border1" Canvas.Left="0" Canvas.Top="0" Width="240"
Height="90" CornerRadius="9">
<Border.Effect>
<DropShadowEffect ShadowDepth="7" BlurRadius="3"
Color="DarkGreen" />
</Border.Effect>
<Border.Background>
<LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">
<GradientStop x:Name="gradient1" Offset="0"
Color="DarkGreen" />
<GradientStop x:Name="gradient2" Offset="0.4" Color="Green" />
<GradientStop x:Name="gradient3" Offset="0.7"
Color="MediumSeaGreen" />
<GradientStop x:Name="gradient4" Offset="0.9"
Color="LightGreen" />
</LinearGradientBrush>
</Border.Background>
<TextBlock HorizontalAlignment="Center" VerticalAlignment="Center"
Text="Event Registration" FontFamily="Comic Sans MS"
FontSize="24" Foreground="Wheat" />
</Border>
</Canvas>
</navigation:Page>
```

code snippet WCFRegistration/Views/Welcome.xaml

Within the Resources section of the Canvas element, two Storyboard elements are defined to do an animation. This is very similar to the animations you saw in Chapter 35 for WPF. Minor differences can be detected between these technologies with animations; for example, the animations with Silverlight don't define the AccelerationRatio and DecelerationRatio properties you know from WPF. However, you can get the same features using key-frame animations or with ease functions. Ease functions were in Silverlight before they became available in WPF, which was extended in .NET 4 to include this feature.

```
<Canvas.Resources>
<Storyboard x:Name="startStoryboard">
<DoubleAnimation From="0" To="400" Duration="00:00:4"
```