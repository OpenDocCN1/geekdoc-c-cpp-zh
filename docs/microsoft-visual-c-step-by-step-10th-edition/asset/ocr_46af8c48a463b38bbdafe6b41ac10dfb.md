```
class Point
{
    private int x, y;
    ...

    public void Deconstruct(out int x, out int y)
    {
        x = this.x;
        y = this.y;
    }
}
```