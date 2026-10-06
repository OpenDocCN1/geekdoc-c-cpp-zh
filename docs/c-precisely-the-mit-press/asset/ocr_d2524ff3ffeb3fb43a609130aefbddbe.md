# Example 84 Struct Value Creation

There are two ways of creating new values of type Frac (145). The first calls the default argumentless constructor, and the second calls the user-defined constructor Frac (long, long).

```
Frac f1 = new Frac();
Frac f2 = new Frac(1,2);
```

# Example 85 Object Creation and Instance Test

# Example 86 Instance Test and Cast: The As Operator

If parameter o cannot be converted to class Point (43), then the result p is null. The test for null in the if statement checks both that it is non-null and that it is a Point.

```
public static void IsNearPoint(Object o) {
Point p = o as Point;
if (p != null && p.x*p.x + p.y*p.y <= 100)
    Console.WriteLine(p + " is a Point near (0,0)");
elelse
    Console.WriteLine(o + " is not a Point or not near (0,0)");
}
```

Example 124 shows another use of the as operator.