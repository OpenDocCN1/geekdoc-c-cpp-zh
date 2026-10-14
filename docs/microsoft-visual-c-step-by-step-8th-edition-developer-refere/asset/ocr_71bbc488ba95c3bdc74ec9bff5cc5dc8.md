and locate the *drawingCanvas_Tapped* method.
This method runs when a user taps the screen or clicks the left mouse button. It draws a square on the screen at the point where the user taps or clicks.

# 8. Locate the statement that calls the *SetLocation* method to set the position of the square on the screen. It is located in the *if* statement block as highlighted in the following:

Click here to view code image

```
if (mySquare is IDraw)
{
    IDraw drawSquare = mySquare;
    drawSquare.SetLocation((int)mouseLocation.X,
(int)mouseLocation.Y);
    drawSquare.Draw(drawingCanvas);
}
```

# 9. Replace this statement with code that sets the *X* and *Y* properties of the *Square* object, as shown in bold in the following code:

Click here to view code image

```
if (mySquare is IDraw)
{
    IDraw drawSquare = mySquare;
    drawSquare.X = (int)mouseLocation.X;
    drawSquare.Y = (int)mouseLocation.Y;
    drawSquare.Draw(drawingCanvas);
}
```

# 10. Locate the *drawingCanvas_RightTapped* method.

This method runs when the user taps and holds a finger on the screen or clicks the right mouse button. It draws a circle at the location where the user taps and holds or right-clicks.

# 11. In this method, replace the statement that calls the *SetLocation* method of the *Circle* object and set the *X* and *Y* properties instead, as shown in bold in the following example:

Click here to view code image

```
if (myCircle is IDraw)
{
    IDraw drawCircle = myCircle;
    drawCircle.X = (int)mouseLocation.X;
    drawCircle.Y = (int)mouseLocation.Y;
    drawCircle.Draw(drawingCanvas);
}
```

# 12. Open the IColor.cs file for the Drawing project in the Code and Text Editor window. This interface specifies the *SetColor* method, like this: