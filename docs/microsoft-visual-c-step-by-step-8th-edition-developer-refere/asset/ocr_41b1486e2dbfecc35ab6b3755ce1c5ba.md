```
using Windows.UI.Xaml.Media;
using Windows.UI.Xaml.Shapes;
using Windows.UI.Xaml.Controls;
```

The purpose of this class is to contain the code common to the Circle and Square classes. A program should not be able to instantiate a DrawingShape object directly.

5. Modify the definition of the DrawingShape class to declare it as abstract, as shown here in bold:

```
abstract class DrawingShape
{
}
```

6. Add the following private variables shown in bold to the DrawingShape class:

Click here to view code image

```
abstract class DrawingShape
{
    protected int size;
    protected int locX = 0, locY = 0;
    protected Shape = null;
}
```

The Square and Circle classes both use the locX and locY fields to specify the location of the object on the canvas, so you can move these fields to the abstract class. Similarly, the Square and Circle classes both use a field to indicate the size of the object when it was rendered; although it has a different name in each class (sideLength and diameter), semantically the field performs the same task in both classes. The name size is a good abstraction of the purpose of this field.

Internally, the Square class uses a Rectangle object to render itself on the canvas, and the Circle class uses an Ellipse object. Both of these classes are part of a hierarchy based on the abstract Shape class in the .NET Framework. The DrawingShape class uses a Shape field to represent both of these types.

7. Add the following constructor to the DrawingShape class:

Click here to view code image

```
abstract class DrawingShape
{
    ...
    public DrawingShape(int size)
    {
        this.size = size;
    }
}
```