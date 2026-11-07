Because myRectangle is an object of type rectangleType, the statement:

`++myRectangle;`

increments the values of the length and width of myRectangle by 1. Moreover, the pointer `this` associated with myRectangle returns the incremented value of myRectangle, which in this case is ignored.

Now, yourRectangle is also an object of type rectangleType, so the statement:

`yourRectangle = ++myRectangle;`

increments the length and width of myRectangle by 1, and the pointer `this` associated with myRectangle returns the incremented value of myRectangle, which is copied into yourRectangle.

# GENERAL SYNTAX TO OVERLOAD THE PRE-INCREMENT OPERATOR ++ AS A MEMBER FUNCTION

The general syntax to overload the pre-increment operator ++ as a member function is described next.

**Function Prototype** (to be included in the definition of the class):

```
className operator++();
```

**Function Definition:**

```
className className::operator++()
{
    // increment the value of the object by 1
    return *this;
}
```

The operator function to overload the pre-increment operator can also be a nonmember of the class rectangleType, which we describe next.

If the operator function `operator++` is a nonmember function of the class rectangleType, it has one parameter, which is an object of type rectangleType. (As before, we assume that the increment operator increments the length and width of a rectangle by 1.)

```
rectangleType operator++(rectangleType rectangle)
{
    // increment the length and width of the rectangle
    (rectangle.length)++;
    (rectangle.width)++;
    return rectangle;  // return the incremented
                       // value of the object
}
```