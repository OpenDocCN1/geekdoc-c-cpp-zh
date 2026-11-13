```
int getColour(){return colour;}
});
```

Thus, constructors can be overloaded in this manner. Constructors are implicitly called when we define objects of their classes:

```
Point WhiteCar; calls Car : : Car()
Point RedCar(2, 3); calls Car : : Car(const int, const int)
```

To create a Point from another Point by copying the properties of one object to a newly created one, the copy process needs to be taken care of. Let us consider the class Point in the following code. In the class Point, we add a third constructor that takes care of copying values from one object to the newly created one.

```
class Point
{
int _x, _y;
public:
Point()
{
_x = _y = 0;
}
Point(const int x, const int y)
{
_x = x;
_Y = y;
}
Point(const Point & from) // Copy constructor
{
_x = from._x;
_y = from._y;
}
void setX(const int val);
void setY(const int val);
int getX()(return _x;)
int getY()(return _y;)
};
```

The third constructor takes a constant reference to an object of class Point as an argument and assigns _x and _y, the corresponding values of the provided object.

This type of constructor is important and is known as the copy constructor. It is highly recommended that each class includes such a constructor, even if it is as simple as the one in the example. The copy constructor is called in the following cases:

```
Point Apoint; calls Point : : Point()
Point Bpoint(apoint); calls Point : : Point(const Point &)
Point Cpoint = Apoint; calls Point : : Point(const Point &)
```

The syntax for writing a copy constructor is as follows:

```
classname(const classname & 0)
{
... 
}
```