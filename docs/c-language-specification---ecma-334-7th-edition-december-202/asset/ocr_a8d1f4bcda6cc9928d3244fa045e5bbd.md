The imagined boxing type described above does not actually exist. Instead, a boxed value of type S has the runtime type S, and a runtime type check using the is operator with a value type as the right operand tests whether the left operand is a boxed version of the right operand. For example,

```
int i = 123;
object box = i;
if (box is int)
{
    Console.Write("Box contains an int");
}
```

will output the following:

Box contains an int

A boxing conversion implies making a copy of the value being boxed. This is different from a conversion of a reference_type to type object, in which the value continues to reference the same instance and simply is regarded as the less derived type object. For example, the following

```
struct Point
{
    public int x, y;

    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

class A
{
    void M()
    {
        Point p = new Point(10, 10);
        object box = p;
        p.x = 20;
        Console.Write(((Point)box).x);
    }
}
```

will output the value 10 on the console because the implicit boxing operation that occurs in the assignment of p to box causes the value of p to be copied. Had Point been declared a class instead, the value 20 would be output because p and box would reference the same instance.

The analogy of a boxing class should not be used as more than a helpful tool for picturing how boxing works conceptually. There are numerous subtle differences between the behavior described by this specification and the behavior that would result from boxing being implemented in precisely this manner.

end note

# 10.2.10 Implicit dynamic conversions

An implicit dynamic conversion exists from an expression of type dynamic to any type T. The conversion is dynamically bound §12.3.3, which means that an implicit conversion will be sought at run-time from the run-time type of the expression to T. If no conversion is found, a run-time exception is thrown.