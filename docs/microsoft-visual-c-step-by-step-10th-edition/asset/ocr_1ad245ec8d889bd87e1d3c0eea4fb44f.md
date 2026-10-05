...

}

Notice that you must specify the class that the Square class inherits from before any interfaces that it implements.

+   3. In the Square class, remove the definitions of the sideLength, rect, locX, and locY fields. These fields are no longer necessary because they are now provided by the DrawingShape class.

+   4. Replace the existing constructor with the following code shown in bold, which calls the base:

Click here to view code image

```
class Square : DrawingShape, IDraw, IColor
{
    public Square(int sideLength)
        : base(sideLength)
    
}
```

Notice that the body of this constructor is empty because the base class constructor performs all initialization required.

+   5. Remove the IDraw.SetLocation and IColor.SetColor methods from the Square class. The DrawingShape class provides the implementation of these methods.

+   6. Modify the definition of the Draw method. Declare it with public override and also remove the reference to the IDraw interface. Again, the DrawingShape class already provides the base functionality for this method, but you will extend it with the specific code required by the Square class.

Click here to view code image

```
public override void Draw(Canvas canvas)
{
    ...
}
```

+   7. Replace the body of the Draw method with the code shown here in bold:

Click here to view code image