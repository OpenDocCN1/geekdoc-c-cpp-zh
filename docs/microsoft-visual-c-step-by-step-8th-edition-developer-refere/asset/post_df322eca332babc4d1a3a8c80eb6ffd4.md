
9. In the list of events, locate the RightTapped event, and then double-click the RightTapped text box.
This event occurs when the user taps, holds, and then releases from the canvas by using his or her finger or clicks the right mouse button on the canvas.

10. Add the following code shown below in bold to the drawingCanvas_RightTapped method:

Click here to view code image

```
private void drawingCanvas_RightTapped(object sender,
RightTappedRoutedEventArgs e)
{
    Point mouseLocation = e.GetPosition(this.drawingCanvas);
    Circle myCircle = new Circle(100);

    if (myCircle is IDraw)
    {
        IDraw drawCircle = myCircle;
        drawCircle.SetLocation((int)mouseLocation.X,
(int)mouseLocation.Y);
        drawCircle.Draw(drawingCanvas);
    }

    if (myCircle is IColor)
    {
        IColor colorCircle = myCircle;
        colorCircle.SetColor(Colors.HotPink);
    }
}
```

The logic in this code is similar to the logic in the drawingCanvas_Tapped method, except that this code draws and fills a circle rather than a square.

11. On the Debug menu, click Start Debugging to build and run the application.

12. When the Drawing Pad window opens, tap or click anywhere on the canvas displayed in the window. A violet square should appear.

13. Tap, hold, and release, or right-click anywhere on the canvas. A pink circle should appear. You can click the left and right mouse buttons any number of times; each click will draw a square or circle at the mouse position. The following image shows the application running on Windows 10:

## Drawing Pad

![](img/16f6e3fe08f01ddadb2741a92c392b0e_361_0.png)

14. Return to Visual Studio and stop debugging.

## Abstract classes

You can implement the ILandBound and IGrazable interfaces discussed before the previous set of exercises in many different classes, depending on how many different types of mammals you want to model in your C# application. In situations such as this, it’s quite common for parts of the derived classes to share common implementations. For example, the duplication in the following two classes is obvious:

[Click here to view code image]()

```
class Horse : Mammal, ILandBound, IGrazable
{
    ...
    void IGrazable.ChewGrass()
    {
        Console.WriteLine("Chewing grass");
        // code for chewing grass
    }
}

class Sheep : Mammal, ILandBound, IGrazable
{
```

```
    ...
    void IGrazable.ChewGrass()
    {
        Console.WriteLine("Chewing grass");
        // same code as horse for chewing grass
    }
}
```

Duplication in code is a warning sign. If possible, you should refactor the code to avoid duplication and reduce any associated maintenance costs. One way to achieve this refactoring is to put the common implementation into a new class created specifically for this purpose. In effect, you can insert a new class into the class hierarchy, as shown by the following code example:

Click here to view code image

```
class GrazingMammal : Mammal, IGrazable
{
    ...
    void IGrazable.ChewGrass()
    {
        // common code for chewing grass
        Console.WriteLine("Chewing grass");
    }
}

class Horse : GrazingMammal, ILandBound
{
    ...
}

class Sheep : GrazingMammal, ILandBound
{
    ...
}
```

This is a good solution, but there is one thing that is still not quite right: you can actually create instances of the GrazingMammal class (and the Mammal class, for that matter). This doesn’t really make sense. The GrazingMammal class exists to provide a common default implementation. Its sole purpose is to be a class from which to inherit. The GrazingMammal class is an abstraction of common functionality rather than an entity in its own right.

To declare that creating instances of a class is not allowed, you can declare that the class is abstract by using the abstract keyword, such as in the following example:

Click here to view code image

```
abstract class GrazingMammal : Mammal, IGrazable
{
    ...
}
```

If you now try to instantiate a *GrazingMammal* object, the code will not compile:

Click here to view code image

```
GrazingMammal myGrazingMammal = new GrazingMammal(...); // illegal
```

## Abstract methods

An abstract class can contain abstract methods. An abstract method is similar in principle to a virtual method (covered in Chapter 12), except that it does not contain a method body. A derived class *must* override this method. An abstract method cannot be private. The following example defines the *DigestGrass* method in the *GrazingMammal* class as an abstract method; grazing mammals might use the same code for chewing grass, but they must provide their own implementation of the *DigestGrass* method. An abstract method is useful if it does not make sense to provide a default implementation in the abstract class but you want to ensure that an inheriting class provides its own implementation of that method.

Click here to view code image

```
abstract class GrazingMammal : Mammal, IGrazable
{
    public abstract void DigestGrass();
    ...
}
```

## Sealed classes

Using inheritance is not always easy and requires forethought. If you create an interface or an abstract class, you are knowingly writing something that will be inherited from in the future. The trouble is that predicting the future is a difficult business. With practice and experience, you can develop the skills to craft a flexible, easy-to-use hierarchy of interfaces, abstract classes, and classes, but it takes effort, and you also need a solid understanding of the problem that you are modeling. To put it another way, unless you consciously design a class with the intention of using it as a base class, it’s extremely unlikely that it will function well as a base class. With C#, you can use the *sealed* keyword to prevent a class from being used as a base class if you decide that it should not be. For example:

Click here to view code image

```
sealed class Horse : GrazingMammal, ILandBound
{
    ...
}
```

If any class attempts to use *Horse* as a base class, a compile-time error will be generated. Note that a sealed class cannot declare any virtual methods and that an

abstract class cannot be sealed.

## Sealed methods

You can also use the sealed keyword to declare that an individual method in an unsealed class is sealed. This means that a derived class cannot override this method. You can seal only a method declared with the override keyword, and you declare the method as sealed override. You can think of the interface, virtual, override, and sealed keywords as follows:

+   - An interface introduces the name of a method.
+   - A virtual method is the first implementation of a method.
+   - An override method is another implementation of a method.
+   - A sealed method is the last implementation of a method.

## Implementing and using an abstract class

The following exercises use an abstract class to rationalize some of the code that you developed in the previous exercise. The Square and Circle classes contain a high proportion of duplicate code. It makes sense to factor this code into an abstract class called DrawingShape because this will help to ease maintenance of the Square and Circle classes in the future.

## Create the DrawingShape abstract class

-   1. Return to the Drawing project in Visual Studio.

### Note

A finished working copy of the previous exercise is available in the Drawing project, which is located in the \Microsoft Press\VCSBS\Chapter 13\Drawing Using Interfaces folder in your Documents folder.

-   2. In Solution Explorer, click the Drawing project in the Drawing solution. On the Project menu, click Add Class.
+   The Add New Item – Drawing dialog box opens.

-   3. In the Name box, type DrawingShape.cs, and then click Add.
+   Visual Studio creates the class and displays it in the Code and Text Editor window.

-   4. In the DrawingShape.cs file, at the list at the top of the file, add the following using directives:

Click here to view code image

```
using Windows.UI;
```
