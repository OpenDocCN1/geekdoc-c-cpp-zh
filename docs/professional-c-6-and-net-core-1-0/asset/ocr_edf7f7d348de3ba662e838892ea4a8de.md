```
foreach (var item in LogicalTreeHelper.GetChildren(grid1).
    OfType<FrameworkElement>().Where(
        e => MyAttachedPropertyProvider.GetMySample(e) !=
string.Empty))
{
    list1.Items.Add(
        $"{item.Name}:
{MyAttachedPropertyProvider.GetMySample(item)}");
}
```

> NOTE Chapter 30, “Styling XAML Apps,” and Chapters 31 through 35 use XAML to show many different attached properties in action —for example, attached properties from container controls such as Canvas, DockPanel, and Grid, but also the ErrorTemplate property from the Validation class.

# Markup Extensions

With markup extensions you can extend XAML with either element or attribute syntax. If an XML attribute contains curly brackets, that’s a sign of a markup extension. Often markup extensions with attributes are used as shorthand notation instead of using elements.

One example of such a markup extension is StaticResourceExtension, which finds resources. Here’s a resource of a linear gradient brush with the key gradientBrush1 (code file MarkupExtensionsUWP/MainPage.xaml):

```
<Page.Resources>
    <LinearGradientBrush x:Key="gradientBrush1"
StartPoint="0.5,0.0" EndPoint="0.5, 1.0">
        <GradientStop Offset="0" Color="Yellow" />
        <GradientStop Offset="0.3" Color="Orange" />
        <GradientStop Offset="0.7" Color="Red" />
        <GradientStop Offset="1" Color="DarkRed" />
    </LinearGradientBrush>
</Page.Resources>
```

This resource can be referenced by using the StaticResourceExtension with attribute syntax to set the Background property of a Button. Attribute syntax is defined by curly brackets and the name of the extension class without the Extension suffix:

```
<Button Content="Test" Background="{StaticResource gradientBrush1}" />
```

WPF also allows the longer form of the attribute shorthand notation with element syntax, as the next code snippet demonstrates. StaticResourceExtension is defined as a child element of the Button.Background element. The property ResourceKey is set with an attribute to gradientBrush1. In the previous example, the resource key is not set with the property ResourceKey (which would be possible as well) but with a constructor overload where the resource key can be set: