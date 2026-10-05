```
abstract class DrawingShape
{
    ...
    public void voidSetLocation(int xCoord, int yCoord)
    {
        this.locX = xCoord;
        this.locY = yCoord;
    }
    public void voidSetColor(Color color)
    {
        if (this.shape is not null)
        {
            SolidColorBrush brush = new SolidColorBrush(color);
            this.shape.Fill = brush;
        }
    }
}
```