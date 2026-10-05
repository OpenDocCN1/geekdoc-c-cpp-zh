14. Return to the DrawingShape class in the Code and Text Editor window.
Replace the SetColor method in this class with the Color property shown here:

Click here to view code image

```
public Color ColorColor{
    set {
        if (this.shape is not null) {
            SolidColorBrush brush = new SolidColorBrush(value);
            this.shape.Fill = brush;
        }
    }
}
```

> Note
The code for the set accessor is almost the same as the original SetColor method except that the statement that creates the SolidColorBrush object is passed the value parameter. Additionally, this is an example where the method syntax is more appropriate than using an expression-bodied member.

15. Return to the DrawingPad.xaml.cs file in the Code and Text Editor window.
in the drawingCanvas_Tapped method, modify the statement that sets the color of the Square object to match the following code in:

Click here to view code image

```
if (mySquare is IColor){
    IColor colorSquare = mySquare;
    colorSquare.Color = Colors.BlueViolet;
}
```

16. Similarly, in the drawingCanvas_RightTapped method, modify the statement that sets the color of the Circle object as shown in bold.