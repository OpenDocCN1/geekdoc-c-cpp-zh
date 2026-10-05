> **Important**
You must call Draw before you call SetColor because the SetColor method sets the color of the Square only if it has already been rendered. If you invoke SetColor before Draw, the color will not be set, and the Square object will not appear.

+   8. Return to the DrawingPad.xaml file in the Design View window, and then select the Canvas object.

+   9. In the list of events, locate the RightTapped event, and then double-click the **RightTapped** box.

This occurs when the user taps, holds, and then releases from the canvas by using a finger or right-clicks on the canvas.

+   10. Add the following code shown in bold to the drawingCanvas_RightTapped method:

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