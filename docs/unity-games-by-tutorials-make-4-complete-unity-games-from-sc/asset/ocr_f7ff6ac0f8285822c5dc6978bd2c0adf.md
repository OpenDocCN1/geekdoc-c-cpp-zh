# Classes

So far, you've seen structures in action, but you also have something called classes.

Underneath Point2D, add the following:

```
class Point2DRef {
    public int X;
    public int Y;

    public void AddPoint(Point2DRef anotherPoint) {
        this.X = this.X + anotherPoint.X;
        this.Y = this.Y + anotherPoint.Y;
    }
}
```

Besides of the class, you will notice the definition is exactly the same as a struct. The big difference between a structure and a class is how they are handled in memory. A structure is a value type, whereas a class is a reference type. A value type exists in the stack, whereas a reference type exists in the heap.

The stack is shortItem term, whereas the heap is designed for long term memory. Ultimately, your structures are meant to handle short-lived objects that represent a value, such as a point in 3D space. A class is meant to exist for larger stretches of your program and tend to be unique, such as a player character.

These types also behave differently.

Add the following in Main() before the closing brace:

```
Point2D yetAnotherPoint = myPoint;
yetAnotherPoint.X = 100;
```

Here, you created a new Point2D object by assigning an existing Point2D object to a variable. When you changed the x property of the new object. When you changed the x property, what do you think happened to the original value?

Add the following to find out:

```
Console.WriteLine(myPoint.X);
Console.WriteLine(yetAnotherPoint.X);
```

Click the Run button and you will see the following results:

| 15 |
| 100 |