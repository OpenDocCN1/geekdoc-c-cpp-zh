```
```csharp
public Label(int x, int y, string caption) {
    this.x = x;
    this.y = y;
    this.caption = caption;
}
public int X {
    get { return x; }
}
public int Y {
    get { return y; }
}
public Point Location {
    get { return new Point(x, y); }
}
public string Caption {
    get { return caption; }
}
}
```
```

Here, the `Label` class uses two `int` fields, `x` and `y`, to store its location. The location is publicly exposed both as an `x` and a `Y` property and as a `Location` property of type `Point`. If, in a future version of `Label`, it becomes more convenient to store the location as a `Point` internally, the change can be made without affecting the public interface of the class:

```
```csharp
class Label
{
    private Point location;
    private string caption;
    public Label(int x, int y, string caption) {
        this.location = new Point(x, y);
        this.caption = caption;
    }
    public int X {
        get { return location.x; }
    }
    public int Y {
        get { return location.y; }
    }
    public Point Location {
        get { return location; }
    }
    public string Caption {
        get { return caption; }
    }
}
```
```

Had `x` and `y` instead been `public readonly` fields, it would have been impossible to make such a change to the `Label` class. *end example*

> > [Note: Exposing state through properties is not necessarily any less efficient than exposing fields directly. In particular, when a property is non-virtual and contains only a small amount of code, the execution environment might replace calls to accessors with the actual code of the accessors. This process is known as *inlining*, and it makes property access as efficient as field access, yet preserves the increased flexibility of properties. *end note*]

[Example: Since invoking a `get` accessor is conceptually equivalent to reading the value of a field, it is considered bad programming style for `get` accessors to have observable side-effects. In the example

```
```csharp
class Counter
{
    private int next;
```
```