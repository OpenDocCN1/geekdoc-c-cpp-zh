```
<Button Content="Test">
    <Button.Background>
        <StaticResourceExtension ResourceKey="gradientBrush1" />
    </Button.Background>
</Button>
```

# Creating Custom Markup Extensions

UWP apps can use only predefined markup extensions. With WPF, you can create custom markup extensions. A markup extension is created by defining a class that derives from the base class MarkupExtension. Most markup extensions have the Extension suffix (this naming convention is similar to the Attribute suffix with attributes, which you can read about in Chapter 16, “Reflection, Metadata, and Dynamic Programming”). With a custom markup extension, you only need to override the method ProvideValue, which returns the value from the extension. The type that is returned is annotated to the class with the attribute MarkupExtensionReturnType. With the method ProvideValue, an IServiceProvider object is passed. With this interface you can query for different services, such as IProvideValueTarget or IXamlTypeResolver. You can use IProvideValueTarget to access the control and property to which the markup extension is applied with the TargetObject and TargetProperty properties. You can use IXamlTypeResolver to resolve XAML element names to CLR objects. The custom markup extension class CalculatorExtension defines the properties X and Y of type double and an Operation property that is defined by an enumeration. Depending on the value of the Operation property, different calculations are done on the X and Y input properties, and a string is returned (code file MarkupExtensionsWPF/CalculatorExtension.cs):

```
using System;
using System.Windows;
using System.Windows.Markup;
namespace Wrox.ProCSharp.XAML
{
    public enum Operation
    {
        Add,
        Subtract,
        Multiply,
        Divide
    }

    [MarkupExtensionReturnType(typeof(string))]
    public class CalculatorExtension: MarkupExtension
    {
        public CalculatorExtension()
        {
        }
        public double X { get; set; }
        public double Y { get; set; }
        public Operation Operation { get; set; }

        public override object ProvideValue(IServiceProvider serviceProvider)
        {

```