```
return Width * Height;
}
class UseRect {
    static void Main() {
        Rect r1 = new Rect(4, 5);
        Rect r2 = new Rect(7, 9);

        Console.WriteLine("Area of r1: " + r1.Area());
        Console.WriteLine("Area of r2: " + r2.Area());
    }
}
```

As you know, within a method, the other members of a class can be accessed directly, without any object or class qualification. Thus, inside Area(), the statement

```
return Width * Height;
```

means that the copies of Width and Height associated with the invoking object will be multiplied together and the result returned. However, the same statement can also be written like this:

```
return this.Width * this.Height;
```

Here, this refers to the object on which Area() was called. Thus, this.Width refers to that object's copy of Width, and this.Height refers to that object's copy of Height. For example, if Area() had been invoked on an object called x, then this in the preceding statement would have been referring to x. Writing the statement without using this is really just shorthand.

It is also possible to use this inside a constructor. In this case, this refers to the object that is being constructed. For example, inside Rect(), the statements

```
Width = w;
Height = h;
```

can be written like this:

```
this.Width = w;
this.Height = h;
```

Of course, there is no benefit in doing so in this case.

For the sake of illustration, here is the entire Rect class written using the this reference:

```
using System;

class Rect {
    public int Width;
    public int Height;

    public Rect(int w, int h) {
```