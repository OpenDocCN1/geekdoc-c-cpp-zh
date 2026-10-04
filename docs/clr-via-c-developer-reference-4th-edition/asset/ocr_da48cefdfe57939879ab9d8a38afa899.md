# Changing Fields in a Boxed Value Type by Using Interfaces (and Why You Shouldn't Do This)

Let's have some fun and see how well you understand value types, boxing, and unboxing. Examine the following code, and whether you can figure out what it displays on the console.

using System;

```
// Point is a value type.
internal struct Point {
    private Int32 m_x, m_y;

    public Point(Int32 x, Int32 y) {
        m_x = x;
        m_y = y;
    }

    public void Change(Int32 x, Int32 y) {
        m_x = x;
        m_y = y;
    }

    public override string ToString() {
        return String.Format("{0}, {1}", m_x.ToString(), m_y.ToString());
    }
}

public sealed class Program {
    public static void Main() {
        Point p = new Point(1, 1);

        Console.WriteLine(p);

        p.Change(2, 2);
        Console.WriteLine(p);

        Object o = p;
        Console.WriteLine(o);

        ((Point)o).Change(3, 3);
        Console.WriteLine(o);
    }
}
```

Very simply, Main creates an instance (p) of a Point value type on the stack and sets its m_x and m_y fields to 1. Then, p is boxed before the first call to WriteLine, which calls ToString on the boxed Point, and (1, 1) is displayed as expected. Then, p is used to call the Change method, which changes the values of p.m_x and m_y on the stack to 2. The second call to WriteLine requires p to be boxed and displays (2, 2), as expected.

Now, p is boxed a third time, and o refers to the boxed Point object. The third call to WriteLine shows (2, 2), which is also expected. Finally, I want to call the Change method to update the fields in the boxed Point object. However, Object (the type of the variable o) doesn't know about the Change method, so I must first cast o to a Point. Casting to a Point unboxes o and