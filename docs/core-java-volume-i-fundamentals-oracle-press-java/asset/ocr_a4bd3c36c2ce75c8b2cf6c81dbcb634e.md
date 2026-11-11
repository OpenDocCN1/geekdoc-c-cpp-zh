Then record instances are mutable:

```
```java
var pt = new PointInTime(0, 0, new Date());
pt.when().setTime(0);
```
```

If you intend record instances to be immutable, don’t use mutable types for fields.

![](bbox=[0.128, 0.295, 0.179, 0.337])

> > **TIP:**
> >
> > Use a record instead of a class for immutable data that is completely represented by a set of variables. Use a class if the data is mutable, or if the representation may evolve over time. Records are easier to read, more efficient, and safer in concurrent programs.

# 4.7.2 Constructors: Canonical, Custom, and Compact

The automatically defined constructor that sets all instance fields is called the *canonical constructor*.

You can define additional *custom constructors*. The first statement of such a constructor must call another constructor, so that ultimately the canonical constructor is invoked. Here is an example:

```
```java
record Point(double x, double y)
{
    public Point() { this(0, 0); }
}
```
```

This record has two constructors: the canonical constructor and a no-argument constructor yielding the origin.

If the canonical constructor needs to do additional work, you can provide your own implementation: