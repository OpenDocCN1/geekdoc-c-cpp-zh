Attached properties are defined very similarly to dependency properties, as shown in the next example. The class that defines the attached properties must derive from the base class `DependencyObject` and defines a normal property, where the get and set accessors invoke the methods `GetValue` and `SetValue` of the base class. This is where the similarities end. Instead of invoking the method `Register` with the `DependencyProperty` class, now `RegisterAttached` is invoked, which registers an attached property that is now available with every element.

```
AttachedPropertyDemo[WPF|UWP]/MyAttachedPropertyProvider.cs:

public class MyAttachedPropertyProvider: DependencyObject
{
    public string MySample
    {
        get { return (string)GetValue(MySampleProperty); }
        set { SetValue(MySampleProperty, value); }
    }

    public static readonly DependencyProperty MySampleProperty =
        DependencyProperty.RegisterAttached(nameof(MySample),
        typeof(string),
        typeof(MyAttachedPropertyProvider), new
        PropertyMetadata(string.Empty);

    public static void SetMySample(UIElement element, string
    value) =>
        element.SetValue(MySampleProperty, value);

    public static int GetMyProperty(UIElement element) =>
        (string)element.GetValue(MySampleProperty);
}
```

> **NOTE** You might assume that `DockPanel.Dock` can only be added to elements within a `DockPanel`. In reality, attached properties can be added to any element. However, no one would use this property value. The `DockPanel` is aware of this property and reads it from its children elements to arrange them.

In the XAML code, the attached property can now be attached to any elements. The second `Button` control, named `button2`, has the property `MyAttachedPropertyProvider.MySample` attached to it and the value 42 assigned.

```
AttachedPropertyDemo[WPF|UWP]/Main[Window|Page].xaml:

<Grid x:Name="grid1">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto" />
        <RowDefinition Height="Auto" />
        <RowDefinition Height="*" />
    </Grid.RowDefinitions>
    <Button Grid.Row="0" x:Name="button1" Content="Button 1" />
    <Button Grid.Row="1" x:Name="button2" Content="Button 2"
            local:MyAttachedPropertyProvider.MySample="42" />
```