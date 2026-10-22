```
double x, y;
Point() : Mixins()..., x(0.0), y(0.0) { }
Point(double x, double y) : Mixins()..., x(x), y(y) { }
};
```

Now, we can “mix in” a base class containing a label to produce a LabeledPoint: [Click here to view code image](#)

```
class Label
{
public:
std::string label;
Label() : label("") { }
};
```

using LabeledPoint = Point<Label>; or even mix in several base classes:

[**Click here to view code image**](#)

```
class Color
{
public:
unsigned char red = 0, green = 0, blue = 0;
};
```

using MyPoint = Point<Label, Color>; with this mixin-based Point, it becomes easy to introduce additional information to Point without changing its interface, so Polygon becomes easier to use and evolve. Users need only apply the implicit conversion from the Point specialization to their mixin class (Label or Color, above) to access that data or interface. Moreover, the Point class can even be entirely hidden, with the mixins provided to the Polygon class template itself: [Click here to view code image](#)

```
template<typename... Mixins>
class Polygon
{
private:
std::vector<Point<Mixins...>> points;
public:
//public operations
};
```

Mixins are useful in cases where a template needs some small level of customization—such as decorating internally stored objects with user-specified data—without requiring the library to expose and document those internal data types and their interfaces.

# 21.3.3.1 Curious Mixins