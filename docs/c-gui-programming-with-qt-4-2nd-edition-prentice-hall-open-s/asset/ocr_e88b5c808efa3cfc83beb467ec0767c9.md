```
Shape.prototype.area = function() { return 0 };

function Circle(x, y, radius) {
  Shape.call(this, x, y);
  this.radius = radius;
}

Circle.prototype = new Shape();
Circle.prototype.area = function() {
  return Math.PI * this.radius;
};
```

We start by defining a Shape constructor and associate an area() function with it, which always returns 0. Then we define a Circle constructor, which calls the base class constructor using the call() function defined for all function objects (including constructors), and we add a radius property. Outside the constructor, we set the Circle's prototype to be a Shape object, and we override Shape's area() function with a Circle-specific implementation. This corresponds to the following C++ code:

Code View:

```
class Shape {
public:
  Shape(double x, double y) {
    this->x = x;
    this->y = y;
  }

  virtual double area() const { return 0; }

  double x;
  double y;
};

class Circle : public Shape {
public:
  Circle(double x, double y, double radius)
    : Shape(x, y) {
    this->radius = radius;
  }
}
```