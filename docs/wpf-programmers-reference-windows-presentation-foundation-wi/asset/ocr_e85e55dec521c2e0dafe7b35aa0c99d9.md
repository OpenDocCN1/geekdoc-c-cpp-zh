# Defining Resources | 195

For example, the following XAML code defines a Resources element that contains RadialGradientBrush named bButton and a BitmapEffectGroup bmeButton. This Resources is contained in the file Window (hence the tag Window.Resources).

```
<Window.Resources>
<LinearGradientBrush x:Key="bButton" StartPoint="0,0" EndPoint="0,1">
  <GradientStop Color="Red" Offset="0"/>
  <GradientStop Color="White" Offset="0.5"/>
  <GradientStop Color="Blue" Offset="1"/>
</LinearGradientBrush>
<BitmapEffectGroup x:Key="bmeButton">
  <DropShadowEffect/>
</BitmapEffectGroup>
</Window.Resources>
```

# ButtonResources

Any object (directly or indirectly) in the object that holds the Resources can use as the resources. In the previous code, the Window contains the Resources element, so any object in the Window can use its resources.

After you have defined a simple property resource as this one, you can use it with property syntax. When you give the attribute should have the format (StaticResource resource_name), where you replace resource_name with the name of the resource.

For example, the following XAML code defines a Button. It sets the Button's Background property to bButton and its BitmapEffect to the bmeButton.

# ButtonResources

The ButtonResources example program shown in Figure 12-1 displays several buttons that use similar code to define their backgrounds and bitmap effects. The only difference between the buttons is the contents of their TextBlocks.

Using resources has several advantages. Because the buttons shown in Figure 12-1 use the same resources, they are guaranteed to have a consistent appearance (at least as far as the Background and BitmapEffect properties are concerned).

![](bbox=[0.498, 0.706, 0.952, 0.915])

Figure 12-1