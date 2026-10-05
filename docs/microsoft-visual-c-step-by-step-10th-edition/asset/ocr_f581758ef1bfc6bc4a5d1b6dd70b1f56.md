```
void IColor.SetColor(Color color)
{
    if (this.circle is not null)
    {
        ColorBrush brush = new SolidColorBrush(color);
        this .circle.Fill = brush;
    }
}
```