This constructor initializes the diameter field.

# 16. Add the following SetLocation method to the Circle class:

Click here to view code image

```
void IDraw.SetLocation(int xCoord, int yCoord)
{
    this.locX = xCoord;
    this.locY = yCoord;
}
```

This method implements part of the IDraw interface, and the code is the same as that in the Square class.

# 17. Add the Draw method shown here to the Circle class:

Click here to view code image

```
void IDraw.Draw(Canvas canvas)
{
    if (this.circle != null)
    {
        canvas.Children.Remove(this.circle);
    }
    else
    {
        this.circle = new Ellipse();
    }

    this.circle.Height = this.diameter;
    this.circle.Width = this.diameter;
    Canvas.SetTop(this.circle, this.locY);
    Canvas.SetLeft(this.circle, this.locX);
    canvas.Children.Add(this.circle);
}
```

This method is also part of the IDraw interface. It is similar to the Draw method in the Square class, except that it renders the Circle object by drawing an Ellipse shape on the canvas. (A circle is an ellipse for which the width and height are the same.)

# 18. Add the following SetColor method to the Circle class:

Click here to view code image

```
void IColor.SetColor(Color color)
{
    if (this.circle != null)
    {
        SolidColorBrush brush = new SolidColorBrush(color);
        this.circle.Fill = brush;
    }
}
```