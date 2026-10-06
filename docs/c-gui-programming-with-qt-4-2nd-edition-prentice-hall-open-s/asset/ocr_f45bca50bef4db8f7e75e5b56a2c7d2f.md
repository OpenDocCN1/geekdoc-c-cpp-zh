```
{
  return xVal;
}
double Point2D::y() const
{
  return yVal;
}
```

We start by including point2d.h because the compiler needs the class definition before it can parse member function implementations. Then we implement the functions, prefixing the function name with the class name using the :: operator.

We have seen how to implement a function inline and now how to implement it in a .cpp file. The two approaches are semantically equivalent, but when we call a function that is declared inline, most compilers simply expand the function's body instead of generating an actual function call. This normally leads to faster code, but might increase the size of your application. For this reason, very short functions should be implemented inline; longer functions should always be implemented in a .cpp file. In addition, if we forget to implement a function and try to call it, the linker will complain about an unresolved symbol.

Now, let's try to use the class.

```
#include "point2d.h"
```

```
int main()
{
  Point2D alpha;
  Point2D beta(0.666, 0.875);

  alpha.setX(beta.y());
  beta.setY(alpha.x());

  return 0;
}
```

In C++, variables of any types can be declared directly without using new. The first variable is initialized using the default Point2D constructor (the constructor that has no parameters). The second variable is initialized using the second constructor. Access to an object's member is performed using the . (dot) operator.