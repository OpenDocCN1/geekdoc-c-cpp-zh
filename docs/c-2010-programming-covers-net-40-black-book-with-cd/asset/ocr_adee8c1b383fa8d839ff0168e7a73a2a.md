# The TextEffect Class

The TextEffect class allows you to add text effects, such as animating and cloning, to text objects, such as TextBlock, TextElement, and FlowDocument. An object of the TextEffect class helps you to treat the text as one or more groups of characters in a text string. The inheritance hierarchy of the TextEffect class is as follows:

```
System.Object
    System.Windows.Threading.DispatcherObject
        System.Windows.DependencyObject
            System.Windows.Freezable
                System.Windows.Media.Animation.Animatable
                    System.Windows.Media.TextEffect
```

The properties of the TextEffect class are listed in Table 11.7:

| Property | Description |
|---|---|
| Clip | Gets or sets the region to apply the text effect |
| Foreground | Gets or sets the Brush object to be applied on the text |
| PositionCount | Gets or sets the position in the text to which the text effect is applied |
| PositionStart | Gets or sets the starting position in the text to apply the text effect |
| Tranform | Gets or sets the transformation that is applied to the text effect |

# The BitMapEffect Class

The BitMapEffect class is an abstract class that allows you to apply visual effects, such as blurs, glows, and drop shadow, to the text. This class provides you an easy and declarative way to enhance the appearance of text. It does not support partial trust execution; therefore, an application must have full trust permission to use BitMapEffect. This implies that you need to have UIPermission to inherit the BitMapEffect class. The UIPermission class controls the permission related to user interface. The inheritance hierarchy of the BitMapEffect class is as follows:

```
System.Object
    System.Windows.Threading.DispatcherObject
        System.Windows.DependencyObject
            System.Windows.Freezable
                System.Windows.Media.Animation.Animatable
                    System.Windows.Media.Effects.BitmapEffect
```

The properties of the BitMapEffect class are listed in Table 11.8:

| Property | Description |
|---|---|
| DependencyObjectType | Retrieves the DependencyObjectType object that wraps the CLR of the current instance |

| Property | Description |
|---|---|
| AngleX | Gets or sets the x-axis skew angle, which is measured in degrees counterclockwise from the y-axis |
| AngleY | Gets or sets the y-axis skew angle, which is measured in degrees counterclockwise from the x-axis |
| CenterX | Gets or sets the x-coordinate of the transform center |
| CenterY | Gets or sets the y-coordinate of the transform center |
| Value | Retrieves the current transformation value |