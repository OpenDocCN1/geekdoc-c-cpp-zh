```
#endif
```

Note the appearance of the `protected` access specifier. The methods in any class derived directly or indirectly from `Rectangle` will be able to access the `length` and `width` fields. These fields will be inaccessible to code outside these classes. Listing 17.22 (`rectangle.cpp`) provides the implementation of `Rectangle`'s methods.

# Listing 17.22: rectangle.cpp

```
// File rectangle.cpp

#include "rectangle.h"
#include <algorithm> // For max function

// Generally for rectangles length >= width, but the
// constructor does not enforce this.
Rectangle::Rectangle(double len, double wid): length(len), width(wid) {}

// Length of the longer side--determine which is longer
double Rectangle::span() const {
  return std::max(length, width);
}

double Rectangle::area() const {
  return length * width;
}
```

From mathematics we know that a square is a special kind of rectangle, so Listing 17.23 (`square.h`) and Listing 17.24 (`square.cpp`) specify a `Square` class.

# Listing 17.23: square.h

```
#ifndef SQUARE_H_
#define SQUARE_H_

#include "rectangle.h"

// A square is a special case of a rectangle
class Square: public Rectangle {
public:
  // Length and width are equal in a square, so specify the
  // length of only one side
  Square(double side);
  // The inherited methods work as is; no need to
  // change their behavior.
};

#endif
```

# Listing 17.24: square.cpp

```
// File square.cpp
```