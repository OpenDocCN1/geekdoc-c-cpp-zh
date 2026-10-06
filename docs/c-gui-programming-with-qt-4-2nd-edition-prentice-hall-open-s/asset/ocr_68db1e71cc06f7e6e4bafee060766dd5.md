| Object | Provides mathematical constants and functions |
| --- | --- |
| Math | |

We have seen how to define a constructor in ECMAScript and how to add member variables to the constructed object. Normally, we also want to define member functions. Because functions are treated as first-class citizens in ECMAScript, this turns out to be surprisingly easy. Here's a new version of the Shape constructor, this time with two member functions annanPos and translate():

```
function Shape(x, y) {
  this.x = x;
  this.y = y;

  this.manhattanPos = function() {
    return Math.abs(this.x) + Math.abs(this.y);
  };
  this.translate = function(dx, dy) {
    this.x += dx;
    this.y += dy;
  };
}
```

We can then invoke the member functions using the . (dot) operator:

```
var shape = new Shape(10, 20);
shape.translate(100, 100);
print(shape.x + ", " + shape.y + " (" + shape.manhattanPos() + ")");
```

With this approach, each Shape instance has its own manhattanPos and translate properties. These properties should be identical for all Shape instances, it is desirable to store them only once rather than in every instance. ECMAScript lets us achieve this by using a prototype. A prototype is an object that serves as a fallback for other objects, providing an initial set of properties. One advantage of this approach is that it is possible to change the prototype object at any time and the changes are immediately reflected in all objects that were created with that prototype.