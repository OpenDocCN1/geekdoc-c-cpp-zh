```
int xpos = origin.X;
origin.Y = -100; // oops
```

The common way to solve this problem is to make the fields private and add an accessor method and a modifier method to read and write the value of each private field, respectively. The modifier methods can then check the range for new field values. For example, the code that follows an accessor (GetX) and a modifier (setX) for the x field. Notice that SetX checks the parameter passed in.

[Click here to view code image](#)

```
struct ScreenPosition
{
    private int X;
    private int Y;
    ...
    public int GetX()
    {
        return this.x;
    }

    public void SetX(int newX)
    {
        this.x = rangeChecked(newX);
    }

    private static int rangeChecked(int x) { }
    private static int rangeCheckedY(int y) { }
    private int x, y;
}
```

The code successfully enforces the range constraints, which is good. However, there's a price to pay for this valuable guarantee: ScreenPosition no longer has a natural field-like syntax. It uses awkward method-based syntax instead.

The example that follows increases the value of x by 10. To do so, it must read the value of x by using the GetX accessor method and then write the value of x by using the SetX modifier method.

```
int xpos = origin.GetX();
origin.SetX(xpos + 10);
```

Compare this with the equivalent code if the x field were public: