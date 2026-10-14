set accessors.

The next code example shows the ScreenPosition structure rewritten by using properties. When looking at this code, notice the following:

+   Lowercase _x and _y are private fields.

+   Uppercase X and Y are public properties.

+   All set accessors are passed the data to be written by using a hidden, built-in parameter named value.

Click here to view code image

```
struct ScreenPosition
{
    private int _x, _y;

    public ScreenPosition(int X, int Y)
    {
        this._x = rangeCheckedX(X);
        this._y = rangeCheckedY(Y);
    }

    public int X
    {
        get { return this._x; }
        set { this._x = rangeCheckedX(value); }
    }

    public int Y
    {
        get { return this._y; }
        set { this._y = rangeCheckedY(value); }
    }

    private static int rangeCheckedX(int x) { ... }
    private static int rangeCheckedY(int y) { ... }
}
```

In this example, a private field directly implements each property, but this is only one way to implement a property. All that is required is for a get accessor to return a value of the specified type. Such a value can easily be calculated dynamically rather than being simply retrieved from stored data, in which case there would be no need for a physical field.

![](bbox=[0.1, 0.77, 0.14, 0.81])

# Note

Although the examples in this chapter show how to define properties for a structure, they are equally applicable to classes; the syntax is the same.