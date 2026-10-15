Now, let’s create a standalone WPF application named SquareBoxDependencyProperty (also available in CD) to demonstrate a custom dependency property. In the code-behind file (MainWindow.xaml.cs), add the following code snippet in the SquareBoxDependencyProperty namespace:

```
public partial class Box : UIElement
{
    public static readonly DependencyProperty BoxHeightProperty;
    public static readonly DependencyProperty BoxWidthProperty;
    public static readonly DependencyProperty IsSquareProperty;
}
```

In the preceding code snippet, a partial class named Box is derived from the UIElement, which inherits the DependencyObject class. In the Box class, three static read-only fields named BoxHeightProperty, BoxWidthProperty, and IsSquareProperty of DependencyProperty type are declared. Note that all three fields are suffixed with the word Property. It is essential to suffix the DependencyProperty fields with the Property word.

If you want to provide validation and coercion on the values of the dependency properties of the Box class, then you need to include the validation and coercion callbacks. The following code snippet shows how to use the validation and coercion in the Box class:

```
public static void IsSquareBoxTrue(DependencyObject myObject, DependencyPropertyChangedEventArgs myObjectArgs)
{
    myObject.CoerceValue(BoxHeightProperty);
    myObject.CoerceValue(BoxWidthProperty);
}
public static object myBoxHeightWidthSquare(DependencyObject myObject, object myValue)
{
    Box box1 = (Box)myObject;
    Boolean square = (Boolean)myValue;
    if (square == true)
        if (box1.BoxHeight > box1.BoxWidth)
            box1.BoxHeight = box1.BoxWidth;
        else
            box1.BoxWidth = box1.BoxHeight;
        return true;
}
public static Boolean IsValidHeight(object height)
{
    if ((int)height <= 0)
        return false;
    else
        return true;
}
public static Boolean IsValidWidth(object width)
{
    if ((int)width <= 0)
        return false;
    else
        return true;
}
```

In the preceding code snippet, the IsSquareBoxTrue() method is the property change callback that has two parameters. The first parameter is of DependencyObject type that refers to an object of the class containing the dependency properties. The second parameter is of DependencyPropertyChangedEventArgs. In the IsSquareBoxTrue method, there are two calls to the CoerceValue() method for BoxHeightProperty and BoxWidthProperty. The CoerceValue() method calls the myBoxHeightWidthSquare() method. The myBoxHeightWidthSquare() method has two parameters of the DependencyObject and object types, respectively. The DependencyObject parameter refers to an object of the Box, while the object parameter refers to the value that is used to coerce the value of other dependency properties. In myBoxHeightWidthSquare() method, if the square variable is true and the BoxHeight property is greater than the BoxWidth property, then the BoxHeight property becomes equal to the BoxWidth property. If the BoxHeight is not greater than the BoxWidth property, then the BoxWidth property is assigned the value of BoxHeight property.