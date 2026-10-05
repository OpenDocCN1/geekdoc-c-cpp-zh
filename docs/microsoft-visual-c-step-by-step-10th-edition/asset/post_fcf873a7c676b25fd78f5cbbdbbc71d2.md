
- 4. In the DrawingShape.cs file, at the list at the top of the file, add the following using directives:

Click here to view code image

```
using Windows.UI;
using Windows.UI.Xaml.Media;
using Windows.UI.Xaml.Shapes;
using Windows.UI.Xaml.Controls;
```

The purpose of this class is to contain the common code to the Circle and Square classes. A program should not be able to instantiate a DrawingShape object directly.

- 5. Modify the definition of the DrawingShape class to declare it as abstract, as shown here in:

```
abstract class DrawingShape
{
}
```

- 6. Add the following protected variables shown in bold to the DrawingShape class:

Click here to view code image

```
abstract class DrawingShape
{
    protected int size;
    protected int locX = 0, locY = 0;
    protected Shape shape = null;
}
```

The Square and Circle classes both use the locX and locY fields to specify the location of the object on the canvas so that you can move these fields to the abstract class. Similarly, the Square and Circle classes both use a field to indicate the size of the object when it was rendered. Although it has a different name in each class (sidelength and diameter), semantically the field performs the same task in both classes. The name size is a good abstraction of the purpose of this field.

Internally, the Square class uses a Rectangle to render itself upon the canvas, and the Circle class uses an Ellipse object. Both of these classes are part of a hierarchy based on the abstract Shape class in .NET. The DrawingShape class uses a Shape field to represent both of these types.

- 7. Add the following constructor to the DrawingShape class:

Click here to view code image

```
abstract class DrawingShape
{
    public DrawingShape(int size)
    {
        this.size = size;
    }
}
```

This code initializes the size field in the DrawingShape object.

- 8. Add the SetLocation and SetColor methods to the DrawingShape class, as shown in bold in the code that follows. These methods provide implementations that are inherited by all classes that derive from the DrawingShape class. Notice that they are not marked as virtual, and a derived class is not expected to override them. Also, the DrawingShape class is not declared as implementing the IDraw or IColor interfaces (interface implementation is a feature of the Square and Circle classes and not this abstract class), so these methods are simply declared as public.

Click here to view code image

```
abstract class DrawingShape
{
    public void SetLocation(int xCoord, int yCoord)
    {
        this.locX = xCoord;
        this.locY = yCoord;
    }
    public void SetColor(Color color)
    {
        if (this.shape is not null)
        {
            SolidColorBrush brush = new SolidColorBrush(color);
            this.shape.Fill = brush;
        }
    }
}
```

- 9. Add the Draw method to the DrawingShape class. Unlike the previous methods, this method is declared as virtual, and any derived classes are expected to override it to extend the functionality. The code in this method verifies that the shape field is not null and then draws it on the canvas. The classes that inherit this method must provide their own code to instantiate the shape object. (Remember that the Square class creates a Rectangle object and the Circle class creates an Ellipse object.)

Click here to view code image

```
abstract class DrawingShape
{
    public virtual void Draw(Canvas canvas)
    {
        if (this.shape is null)
        {
            throw new InvalidOperationException("Shape is null");
        }

        this.shape.Height = this.size;
        this.shape.Width = this.size;
        Canvas.SetTop(this.shape, this.locY);
        Canvas.SetLeft(this.shape, this.locX);
        canvas.Children.Add(this.shape);
    }
}
```

You've now completed the DrawingShape abstract class. The next steps are to change the Square and Circle classes so that they inherit from this class and to remove the duplicated code from the Square and Circle classes.

## To modify the Square and Circle classes to inherit from the DrawingShape class

- 1. Display the code for the Square in the Code and Text Editor window.
- 2. Modify the definition of the Square class so that it inherits from the DrawingShape class in addition to implementing the IDraw and IColor interfaces.

Click here to view code image

```
class Square : DrawingShape, IDraw, IColor
{
```

...

}

Notice that you must specify the class that the Square class inherits from before any interfaces that it implements.

- 3. In the Square class, remove the definitions of the sideLength, rect, locX, and locY fields. These fields are no longer necessary because they are now provided by the DrawingShape class.

- 4. Replace the existing constructor with the following code shown in bold, which calls the base:

Click here to view code image

```
class Square : DrawingShape, IDraw, IColor
{
    public Square(int sideLength)
        : base(sideLength)
    
}
```

Notice that the body of this constructor is empty because the base class constructor performs all initialization required.

- 5. Remove the IDraw.SetLocation and IColor.SetColor methods from the Square class. The DrawingShape class provides the implementation of these methods.
- 6. Modify the definition of the Draw method. Declare it as virtual and also remove the reference to IDraw interface. DrawingShape class already provides the functionality, but you will extend it with the specific code:

```
public virtual void Draw(Canvas canvas)
{
```

- 7. Replace the body of the Draw method with the code shown here:

Click here to view image

```
public override void Draw(Canvas canvas)
{
    if (this.shape is null)
    {
        throw new InvalidOperationException("Shape is null");
    }

    this.shape.Height = this.size;
    this.shape.Width = this.size;
    Canvas.SetTop(this.shape, this.locY);
    Canvas.SetLeft(this.shape, this.locX);
    canvas.Children.Add(this.shape);
}
```

These statements instantiate the shape field as a new Rectangle in the Square class.

- 8. Repeat steps 2 through 7 for the Circle class, except that the constructor should be called with diameter, and in the Draw method, you should instantiate the shape field as new Ellipse. The complete code for Circle should look like this:

```
class Circle : DrawingShape, IDraw, IColor
{
    public Circle(int diameter)
        : base(diameter)
    {
    }

    public override void Draw(Canvas canvas)
    {
        if (this.shape is null)
        {
            throw new InvalidOperationException("Shape is null");
        }

        this.shape.Height = this.size;
        this.shape.Width = this.size;
        Canvas.SetTop(this.shape, this.locY);
        Canvas.SetLeft(this.shape, this.locX);
        canvas.Children.Add(this.shape);
    }
}
```

- 9. On the Debug menu, select Debugging.

10. When the Drawing Pad window opens, verify that Square objects appear when you left-click in the window, and Circle objects appear when you right-click. The application should behave the same as before.

11. Return to Visual Studio and stop debugging.

# Compatibility with the Windows Runtime revisited

Chapter 9, “Creating value with enumerations and structures,” described how the Windows platform from 8 onward implements the Windows Runtime (WinRT) as a layer on top of the native APIs, providing a simplified programming interface for developers building unmanaged applications.

.NET provides an extensive set of libraries and features. On Windows 7 and earlier versions, the CLR implements these features by the native Windows APIs. If you’re building desktop or enterprise applications and services on Windows 11, this same feature set is still available (although .NET itself has been upgraded to version 6), and any C# applications that work on Windows 7 should run unchanged.

On Windows 11, UWP apps always run using WinRT. This means that if you’re building UWP apps using a managed language as C#, the CLR actually invokes WinRT rather than the native APIs. Microsoft provides a mapping layer between the CLR and WinRT that can transparently translate requests to create .NET objects and invoke .NET methods into the equivalent object requests and method calls in WinRT. When you create an Int32 value (an int in C#), this code is translated to create a value using the equivalent WinRT data type.

Although the CLR and WinRT have a large amount of overlapping functionality, not all the features of .NET have corresponding features in WinRT. Consequently, UWP apps have access to only a reduced subset of the types and methods provided by .NET.
