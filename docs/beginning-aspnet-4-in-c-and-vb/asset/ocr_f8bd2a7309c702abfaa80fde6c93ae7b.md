```
{
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();

            MyAttachedPropertyProvider.SetMyProperty(button1, 44);

            foreach (object item in LogicalTreeHelper.GetChildren(grid1))
            {
                FrameworkElement e = item as FrameworkElement;
                if (e != null)
                {
                    list1.Items.Add(String.Format("({0}): {1}", e.Name,
                        MyAttachedPropertyProvider.GetMyProperty(e)));
                }
            }
        }
    }
}
```

code snippet AttachedPropertyDemo/MainWindow.xaml.cs

> There are some mechanisms available to extend classes at a later time. Extension methods can be used to extend any class with methods. Extension methods only support extending classes with methods, not properties. Extension methods are explained in Chapter 3, "Objects and Types." The ExpandObject class allows the extension of types with methods and properties. To use this feature, the class must derive from ExpandObject. ExpandObject and dynamic types are explained in Chapter 12, "Dynamic Language Extensions."

> Chapters 35 and 36 show many different attached properties in action, for example attached properties from container controls such as Canvas, DockPanel, Grid, but also the ErrorTemplate property from the Validation class.

# MARKUP EXTENSIONS

With markup extensions you can extend XAML, with either element or attribute syntax. If an XML attribute contains curly brackets, that's a sign of a markup extension. Often markup extensions with attributes are used as shorthand notation instead of using elements.

One example of such a markup extension is StaticResourceExtension, which finds resources. Here's a resource of a linear gradient brush with the key gradientBrush.

```
<Window.Resources>
    <LinearGradientBrush x:Key="gradientBrush" StartPoint="0.5,0.0" EndPoint="0.5, 1.0">
        <GradientStop Offset="0" Color="Yellow" />
        <GradientStop Offset="0.3" Color="Orange" />
        <GradientStop Offset="0.7" Color="Red" />
        <GradientStop Offset="1" Color="DarkRed" />
    </LinearGradientBrush>
</Window.Resources>
```

code snippet MarkupExtensionDemo/MainWindow.xaml